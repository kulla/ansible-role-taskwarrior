taskwarrior
===========

Installs and configures the task management tool [taskwarrior](https://taskwarrior.org/).

Role Variables
--------------

The main variables for configuring this role are:

```yaml
# Defines for which user taskwarrior shall be configured
# (This variable defaults to the value of the variable "ansible_user_id")
taskwarrior_user_id: "{{ ansible_user_id }}"

# Configuration for taskwarrior
taskwarrior_configuration:
```

There can find more variables for a more specialized configuration in [`defaults/main.yml`](defaults/main.yml). Normally you will not need to use these variables.

Example Playbook
----------------

```yaml
- hosts: localhost
  roles:
     - taskwarrior
  vars:
    taskwarrior_user_id: myusername

    taskwarrior_configuration: |
      # -- My configuration of taskwarrior --
      weekstart=Sunday

      color.tag.important=bold white on rgb010

      context.work=project:work or +important
```

Dependencies and Requirements
-----------------------------

This role has no dependencies or requirements.

License
-------

To the extent possible under law, I waive all copyright and related or neighboring rights to this software stored under [https://github.com/kulla/ansible-role-taskwarrior](https://github.com/kulla/ansible-role-taskwarrior). Thus, I publish this software under the [CC0 1.0 Universal (CC0 1.0) Public Domain Dedication](https://creativecommons.org/publicdomain/zero/1.0/deed.en). This software is published from Germany.

Author Information
------------------

[Stephan Kulla](http://kulla.me/)
