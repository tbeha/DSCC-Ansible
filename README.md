# DSCC-Ansible
Ansible playbooks for the Data Services Cloud Console (DSCC)

The playbooks just use builtin Ansible routines and do not require any additional DSCC python SDKs to be installed. The approach for these DSCC Ansible playbooks was to use the ansible.builtin.uri method to access the DSCC API. 

The DSCC API documentation can be found at: https://console-us1.data.cloud.hpe.com/doc/api/v1/

The actual ansible.builtin.uri calls are consolidate in three base playbooks:

| Basic Playbook    | Required Parameter                   | Optional Parameter       | Description           | 
|-------------------|--------------------------------------|--------------------------|-----------------------|
|DSCC-API-Call.yaml | requestUri: the request URL          | body: the request body   |issues a REST API call |
|                   | method: the request method (GET, POST, DELETE, PUT)   |       |           |
|DSCC-API-401.yaml  | requestUri: the request URL          | body: the request body   |Gets a new access token and issues a REST API Call|
|                   | method: the request method (GET, POST, DELETE, PUT)  |      |  |
|Get-Token.yaml     |           |              |Retrieves an access token and store is in token.txt|





## Contact
Thomas Beha - t.beha@t-online.de

Project Link: https://github.com/tbeha/DSCC-Ansible 