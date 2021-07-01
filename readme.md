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
| groups.create.name      | yes      | N/A     | string                    | the group name                           |
| groups.create.gid       | yes      | N/A     | integer                   | the group id                             |
| groups.create.password_login | yes | N/A     | yes, no                   | the groups ability to login via ssh with as password |
| groups.create.sudo_content | yes   | N/A     | list of strings           | content to add to /etc/sudoers/groupname using a template |
| groups.remove           | no       | N/A     | list of strings           | the groups to remove                     |
| groups.sudo.enabled     | no       | N/A     | true, false               | install and configure sudo for groups    |

```yaml
groups:
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
