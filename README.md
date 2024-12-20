# DSCC-Ansible
Ansible playbooks for the Data Services Cloud Console (DSCC)

The playbooks just use builtin Ansible routines and do not require any additional DSCC python SDKs to be installed. The approach for these DSCC Ansible playbooks was to use the ansible.builtin.uri method to access the DSCC API. 

The DSCC API documentation can be found at: https://console-us1.data.cloud.hpe.com/doc/api/v1/

Common tasks are stored in the following base playbooks:

| Basic Playbook    | Required Parameter                   | Optional Parameter       | Description                                                                       | 
|-------------------|--------------------------------------|--------------------------|-----------------------------------------------------------------------------------|
|DSCC-API-Call | requestUri: the request URL          | body: the request body   |issues a REST API call |
|                   | method: the request method (GET, POST, DELETE, PUT)   |       |           |
|DSCC-API-401 | requestUri: the request URL          | body: the request body   |Gets a new access token and issues a REST API Call|
|                   | method: the request method (GET, POST, DELETE, PUT)  |      |  |
|Get-Token|           |              |Retrieves an access token and store is in token.txt|
|DisplayResults| result: the rcommand response | elements: a shortened response output| Displays the response of the last call|
|  | elementname: desriptive name of the result | | |

The base playbooks are used by the task specific playbooks. The following tasks are currently available as playbooks: 

| Playbook    | Required Parameter                   | Optional Parameter       | Description           | 
|-------------------|--------------------------------------|--------------------------|-----------------------|
| Get-Access-Token  |  |  | Getss a new access token |
| Get-AuditEvents  |  | Limit: (50) the number of events to retrieve | Gets the last audit events |
| Get-Host-Duplicates  |  |  | Gets the list of host duplicates  |
| Get-HostGroup-Details  | HostGroupName  |  | Gets the details of the host group with name __HostGroupName__   |
| Get-HostGroups |  |  | Gets all host groups |
| Get-Hosts |  | offset: (0) limit: (100)  |  Gets list of hosts |
| Get-Initiators  |  | offset: (0) limit: (250)  |  Gets list of initiators |
| Get-Snapshot-Details | VolumeName, SnapshotName or SnapshotId |  | Gets the details of the snapshot defined by __VolumeName__ and __SnapshotName__ or __SnapshotId__  |
| Get-System-Capacity | SystemName |  | Gets the capacity details of the storage system identified by __SystemName__ |
| Get-SystemVolumes | SystemName |  | Get the volumes of a storage system identified by __SystemName__ |
| Get-Systems  |  |  | Retrieves all storage systems of an DSCC and stores a dictionary of the storage systems in __systems.json__  |
| Get-Task-Details | taskid |  | Retrieves the detailed information of a task identified by __taskid__|
| Get-Tasks |  | offset: (0) limit: (50) | Get the latest tasks and stores it in __tasks.json__  |
| Get-Volume-Details | VolumeName  |  | Get the details of the Volume identified by __VolumeName__ |
| Get-Volume-Snapshots | VolumeName |  | Get the Snapshots of the Volume identified by __VolumeName__ |
| Get-Volumes |  | offset: (0) limit: (250)  | Get the list of volumes |
| Create-Host | name: name of the host, os: AIX, Apple, Citrix Hypervisor(XenServer), HP-UX, IVM VIO Server, InForm, NetApp/ONTAP, OE Linux UEK, OpenVMS,Oracle VM x86, RHE Linux, RHE Virtualization, Solaris, SuSe Linux, SuSe Virtualization, Ubuntu, VMware (ESXi), Windows Server | comment, contact, fqdn, hostGroupIds, initiatorIds, initiatorsToCreate, ipAddress, location, persona, subnet | Creates a new Host: ansible-playbook Create-Host.yaml -e '{"hostName": " ...", "comment":"Thomas Beha","hostIds":["f296b54a83450f32616f7a33","82a98411f506f648c114fd5b913bc8a8"]}'  |
| Create-HostGroup | Name | comment, hostIds, hostsToCreate  | ansible-playbook Create-HostGroup.yaml -e '{"hostgroupName": "KVMcluster", "comment":"Thomas Beha", "hostIds":["c81bc3f1f296b54a83450f32616f7a33","82a98411f506f648c114fd5b913bc8a8","e9cc50a6b7dadbbf514f3a02196a6596"]}' |
| Create-Initiator | address - Initiator address, protocol - FC/iSCSI/NVMe  | ipAddress, Name |  ansible-playbook Create-Initiato.yaml -e "Address=' ' Protocol=' '..." |
| Create-Snapshot | VolumeName, NamePattern - Name pattern: "PARENT_TIMESTAMP", "PARENT_SEC_SINCE_EPOCH", "CUSTOM" | Comment - string or null, CustomName - Snapshot Name or null, ExpireSecs - Expiration time ins seconds, ReadOnly - Boolean, RetainSecs / Retention time in seconds  | ansible-playbook Create-Snapshot.yaml -e "VolumeName='AnsibleTestVolume_01' ..." |
| Create-Volume | SystemName  name of the storage system, VolumeName  name of the volume | Size - Size (in MiB) of the volume to be created (116384 MiB=16GiB), CPG - User CPG (SSD_r6), Comment, Count (1), DataReduction (true), UserAllocWarning (5), SnapshotAllocWarning (5) | ansible-playbook Create-Volume.yaml -e "SystemName='CTC-MP-Block8' VolumeName='AnsibleTestVolume_01' CPG='SSD_r6' Size='20480' Comment='Ansible Test Thomas Beha' Count='1' DataReduction='true'"  |
| Delete-HostGroup | hostgroupName | Force (true) | ansible-playbook Create-HostGRoup -e "hostgroupName=' ' Force='true'"  |
| Delete-Initiator | initiatorId | Force  (true) | ansible-playbook Delete-Initiator -e "initiatorId=' '"  |
| Delete-Volume-Snapshot | VolumeName, SnapshotName | | ansible-playbook Delete-Volume-Snapshot.yaml -e "VolumeName='...' SnapshotName='...'" |
| Delete-Volume | VolumeName | Unexport (true), Cascade (true) | ansible-playbook DeleteVolume.yaml -e "VolumeName='<volumeName>'"  |
| Export-Volume-Snapshot | VolumeName, SnapshotName, HostGroupName  |  | ansible-playbook Export-Volume-Snapshot.yaml -e "VolumeName=' '..." |
| Export-Volume | VolumeName, HostGroupName | LUN - Custom LUN Id for multiple host groups (Array of objects or null), autoLun (true), maxAutoLun, proximity - Host proximity setting for Active Peer Persistence configuration (__PRIMARY__ , SECONDARY, ALL) | ansible-playbook Export-Volume.yaml -e "VolumeName='<volumeName>' HostGroupName='<hostgroupName>" |
| UnExport-Volume-Snapshot | SnapshotName, HostGroupName  |  |  |
| UnExport-Volume | VolumeName, HostGroupName |  | ansible-playbook UnExport-Volume.yaml -e "VolumeName='<volumeName>' HostGroupName='<hostgroupName>" |
| Update-HostGroup | hostgroupName | hostsToCreate - list of hosts to be added to the group, updatedHosts - Array of strings or null; list of host ids added to the group, removedHosts - Array of strings or null; list of host ids to be removed from group, hostProximity - Array of object or null; change proximity for list of hosts | ansible-playbook Update-HostGroup.yaml -e '{"updatedHosts":"host1","removedHosts":"host2","hostProximity":[{"groupName": "RCGName", "groupUid":"rcg1"}],"hostsToCreate":[{"initiatorIds":"id","name":"Hostname"}]}' |
| Merge-Duplicates |  |  | ansible-playbook Merge-Duplicates.yaml |
| Restore-Volume-Snapshot | VolumeName, SnapshotName | | Restores the volume (identified by __VolumeName__) with the snapshot identified by __SnapshotName__ |
| Show-Data | filename |  | ansible-playbook Show-Data.yaml -e "filename='storage.json'" |
| Search-Data | filename, searchKey |  | ansible-playbook Search-Data.yaml -e "filename='volumes.json' searchKey='MVMn1'" |


Besides these common tasks a complete DSCC Capture is available too. This includes the following components of the repository:

| Playbook          | Description                    | Required Parameter  |
|-------------------|------------------------------|-----------------|
| Capture-Systems.yaml | The DSCC capture script calling the following subroutines. The results are stored in multiple json files (Outputs/<systemname>.<subname>.json) |   no parameter required         |
|  DSCC-API-Call    | the calling routins providing the necessary parameter for the API calls | base_url and access credentials stored in an Ansible vault file: vars/credentials.yml |
|  Loop-Systems.yaml | loops through all known storage systems of the DSCC | |
|  Loop-Links.yaml | loops through all associated links of a storage system. This routine is called in Loop-Systems.yaml | |
|  GetAllSystemsVolumes.yaml | retrieves the information of all volumes of a storage system. | |
|  GetAllHosts.yaml | retrieves all known DSCC hosts | |
|  GetAllHostGroups.yaml | retrieves all known DSCC hostgroups | |


## Contact
Thomas Beha - t.beha@t-online.de

Project Link: https://github.com/tbeha/DSCC-Ansible 
