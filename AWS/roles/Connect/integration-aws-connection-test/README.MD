Role Name
=========

AWS connection validation

Requirements
------------
N/A

Role Notes
------------

This role tests connection  


Role Variables
--------------

Default values are in `defaults/main.yml`.  
Listed below are all variables defined in this role.

```yaml
target_aws_region: us-east-2

Role Templates
--------------
N/A


Tags
------------
N/A

Dependencies
------------

See Requirements section

Example Playbook
----------------

    - hosts: localhost
      roles:
         - integration-aws-connection-test

License
-------

 For Comerica Internal Use Only

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
