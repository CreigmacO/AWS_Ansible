Role Name
=========

App deploy role for CMA Roles

Requirements
------------

None

Role Notes
--------------
This role is a first-pass at completing app deploys with Ansible in place of the current bash script. At this time, it does not yet perform the app deploy. It templates out the app deploy files that tell the deploy script which servers and which JVMs to target for a given application.
##### Note:
This role expects downstream applications to have an inventory group called "deployment-manager".  
For dev, this should be the appserver(s).  
For QA and above this should be "localhost" to avoid SSH connectivity failures.

Role Variables
--------------

Default values are in `defaults/main.yml`.

These are the variables included in this role:

```yaml
#global vars
jenkins_build_path: "/cma/wlpbuilds/jenkins/"
jenkins_deploy_path: "/cma/wlpbuilds/jenkins/{{env_name | upper}}/"
liberty_user_name: wlpadm{{env_suffix_char}}
liberty_group_name: wlpadm{{env_suffix_char}}

app_name: someApplicationName

deployment_manager_hostname: "{{hostvars[groups['deployment-manager'][0]]['inventory_hostname']}}"

jenkins_deploy_files:
  - { src: AppNameEnv.jvm.names.j2, dest: "{{jenkins_build_path}}/{{app_name}}/{{app_name}}{{env_name|upper}}.jvm.names" }
  - { src: AppNameEnv.server.names.j2, dest: "{{jenkins_build_path}}/{{app_name}}/{{app_name}}{{env_name|upper}}.server.names" }

```
------------

Tags
------------
Tags in this role | Targeted components
------------ | -------------
deployfiles | populates app deploy files on the deployment manager  

Dependencies
------------

See Requirements section

Example Playbook
----------------

    - hosts: servers
      roles:
         - integration-app-deploy

Role Files and Templates
--------------
This role templates out 2 files:
  - AppNameEnv.jvm.names
  - AppNameEnv.server.names

It populates the server names using the inventory hosts file taking the servers within the provided group name.



License
-------

 For Comerica Internal Use Only

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
