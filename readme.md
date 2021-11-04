Groups Role
=========

The groups role will create and remove groups, and manage their sudo settings if configured to do so via variables.

[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-neoloc.groups-blue.svg)](https://galaxy.ansible.com/neoloc/ansible-role-groups/)


Requirements
------------

All included in ansible-base package.

Role Variables
--------------

An example list of all variables for this role should go here, including any variables that are in defaults/main.yml and vars/main.yml. Any variables that are read from other roles and/or the global scope (e.g. hostvars, groupvars, etc) should be shown here also.

| Variable                | Required | Default | Choices                   | Comments                                 |
|-------------------------|----------|---------|---------------------------|------------------------------------------|
| groups_all.create.name      | yes      | N/A     | string                    | the group name                           |
| groups_all.create.gid       | yes      | N/A     | integer                   | the group id                             |
| groups_all.create.password_login | yes | N/A     | yes, no                   | the groups ability to login via ssh with as password |
| groups_all.create.sudo_content | yes   | N/A     | list of strings           | content to add to /etc/sudoers/groupname using a template |
| groups_all.remove           | no       | N/A     | list of strings           | the groups to remove                     |
| groups_all.sudo.enabled     | no       | N/A     | true, false               | install and configure sudo for groups    |
| groups_group.create.name      | yes      | N/A     | string                    | the group name                           |
| groups_group.create.gid       | yes      | N/A     | integer                   | the group id                             |
| groups_group.create.password_login | yes | N/A     | yes, no                   | the groups ability to login via ssh with as password |
| groups_group.create.sudo_content | yes   | N/A     | list of strings           | content to add to /etc/sudoers/groupname using a template |
| groups_group.remove           | no       | N/A     | list of strings           | the groups to remove                     |
| groups_group.sudo.enabled     | no       | N/A     | true, false               | install and configure sudo for groups    |
| groups_host.create.name      | yes      | N/A     | string                    | the group name                           |
| groups_host.create.gid       | yes      | N/A     | integer                   | the group id                             |
| groups_host.create.password_login | yes | N/A     | yes, no                   | the groups ability to login via ssh with as password |
| groups_host.create.sudo_content | yes   | N/A     | list of strings           | content to add to /etc/sudoers/groupname using a template |
| groups_host.remove           | no       | N/A     | list of strings           | the groups to remove                     |
| groups_host.sudo.enabled     | no       | N/A     | true, false               | install and configure sudo for groups    |


Role Variables Examples
-----------------------

```yaml
# in group_vars/all.yml
groups_all:
  create:
    - name: admins
      gid: 3001
      password_login: no
      sudo_content:
        - ALL=(ALL) NOPASSWD:ALL
    - name: operators
      gid: 3002
      password_login: no
      sudo_content:
        - ALL = (root) NOPASSWD: /usr/local/bin/custom-tool
        - ALL = (root) NOPASSWD: /usr/sbin/something with-specific-arguments
        - ALL = (root) NOPASSWD: /usr/local/bin/other-thing
  remove:
    - group1
    - group2
    - othergroup
  sudo:
    enabled: true
```

```yaml
# in group_vars/group_name.yml
groups_group:
  create:
    - name: group_admins
      gid: 4001
      password_login: no
      sudo_content:
        - ALL=(ALL) NOPASSWD:ALL
    - name: operators
      gid: 3002
      password_login: no
      sudo_content:
        - ALL = (root) NOPASSWD: /usr/local/bin/custom-tool
        - ALL = (root) NOPASSWD: /usr/sbin/something with-specific-arguments
        - ALL = (root) NOPASSWD: /usr/local/bin/other-thing
  remove:
    - group1
    - group2
    - othergroup
  sudo:
    enabled: true
```

```yaml
# in host_vars/hostname.yml
groups_host:
  create:
    - name: host_admins
      gid: 2001
      password_login: no
      sudo_content:
        - ALL=(ALL) NOPASSWD:ALL
    - name: operators
      gid: 3002
      password_login: no
      sudo_content:
        - ALL = (root) NOPASSWD: /usr/local/bin/custom-tool
        - ALL = (root) NOPASSWD: /usr/sbin/something with-specific-arguments
        - ALL = (root) NOPASSWD: /usr/local/bin/other-thing
  remove:
    - group1
    - group2
    - othergroup
  sudo:
    enabled: true
```

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - neoloc.groups

License
-------

See license.md

Author Information
------------------

[![Github](https://img.shields.io/badge/Github-neoloc-blue.svg)](https://github.com/neoloc)
