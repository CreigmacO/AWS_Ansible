Role Name
=========

List tags and hosts role for CMA Roles

Requirements
------------

None

Role Notes
--------------
This role prints comma-separated lists of all unique tags and hosts for a given playbook.  
Jenkins should generate the `.properties` files in one job and reference them as extended choice parameters in another.
It does not require connectivity to the target servers because all actions are done locally on the Ansible server.

Role Variables
--------------

Default values are in `defaults/main.yml`.

These are the variables included in this role:

```yaml
#a space-separated list of playbooks for tag capture
playbook_names_list: jvms.yml
inventory_name: dev

#intermediate variable do not reference for use
all_tags: '{{tags_output.stdout_lines |join(",")| regex_replace("(.*?\sTAGS:\s)(\[)(.*?)(\])", "\3,")}}'

#string glob of all tags found for a given playbook
all_tags_no_space: '{{all_tags|regex_replace("(.*?,)\s", "\1")}}'

#final comma-separated list of tags. Includes trailing comma.
unique_tags_list: '{{all_tags_no_space.split(",")|unique | difference("codecheckout") | join(",") }}'

#hosts

#intermediate variable do not reference for use
all_hosts: '{{hosts_output.stdout_lines |join(",")| regex_replace("(.*?\s)(pattern:\s\[u'')(.*?)(''\],\s+)(hosts\s\(\d\):,)(\s+)([a-zA-Z\d]+)", "\7,\3,")}}'

#final comma-separated list of hosts. Includes trailing comma.
unique_hosts_list: '{{all_hosts.split(",")|unique | join(",") }}'

```
Downstream roles should only need to provide the playbook name.


Tags
------------
Tags in this role | Targeted components
------------ | -------------
tagslist | lists all tags

Dependencies
------------

See Requirements section

Example Playbook
----------------

    - hosts: localhost
      roles:
         - integration-list-tags




License
-------

 For Comerica Internal Use Only

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
