# DSCC-Ansible
Ansible playbooks for the Data Services Cloud Console (DSCC)

The playbooks just use builtin Ansible routines and do not require any additional DSCC python SDKs to be installed. The approach for these DSCC Ansible playbooks was to use the ansible.builtin.uri method to access the DSCC API. 

The DSCC API documentation can be found at: https://console-us1.data.cloud.hpe.com/doc/api/v1/

Common tasks are stored in the following base playbooks:

| Basic Playbook    | Required Parameter                   | Optional Parameter       | Description           | 
|-------------------|--------------------------------------|--------------------------|-----------------------|
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
| Create-HostGroup |  |  |  |
| Create-Initiator |  |  |  |
| Create-Snapshot |  |  |  |
| Create-Volume |  |  |  |
| Delete-HostGroup |  |  |  |
| Delete-Initiator |  |  |  |
| Delete-Volume |  |  |  |
| Export-Volume-Snapshot |  |  |  |
| Export-Volume |  |  |  |
| UnExport-Volume-Snapshot |  |  |  |
| UnExport-Volume |  |  |  |
| Update-HostGroup |  |  |  |
| Merge-Duplicates |  |  |  |
| Show-Data |  |  |  |
| Search-Data |  |  |  |



## Contact
Thomas Beha - t.beha@t-online.de

Project Link: https://github.com/tbeha/DSCC-Ansible 
