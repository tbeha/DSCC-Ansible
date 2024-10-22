# DSCC-Ansible
Ansible playbooks for the Data Services Cloud Console (DSCC)

The playbooks just use builtin Ansible routines and do not require any additional DSCC python SDKs to be installed. The approach for these DSCC Ansible playbooks was to use the ansible.builtin.uri method to access the DSCC API. 

The DSCC API documentation can be found at: https://console-us1.data.cloud.hpe.com/doc/api/v1/

The actual ansible.builtin.uri calls are consolidate in three base playbooks:


