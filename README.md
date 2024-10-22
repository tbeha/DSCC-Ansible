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
| Get-System-Capacity |  |  |  |
| Get-SystemVolumes |  |  |  |
| Get-Systems  |  |  |   |
| Get-Task-Details |  |  |
| Get-Tasks |  |  |  |
| Get-Volume-Details |  |  |  |
| Get-Volume-Snapshots |  |  |  |
| Get-Volumes |  |  |  |
| Create-Host |  |  |  |
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
