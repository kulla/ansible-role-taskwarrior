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

# Set to true, if a hourly cronjob for syncing shall be configured
taskwarrior_cronjob_sync:

# Configuration for taskwarrior
taskwarrior_configuration:

# Name of taskserver's certificate (taskd.ca)
taskwarrior_server_certificate:

# Name of client's certifiacte (taskd.certificate)
taskwarrior_client_certificate:

# Name of client's key (taskd.key)
taskwarrior_client_key:
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

    taskwarrior_server_certificate: ca.cert.pem
    taskwarrior_client_certificate: first_last.cert.pem
    taskwarrior_client_key: first_last.key.pem

    taskwarrior_configuration: |
      # -- My configuration of taskwarrior --
      weekstart=Sunday

      color.tag.important=bold white on rgb010

      context.work=project:work or +important

    taskwarrior_cronjob_sync: true
```

The taskwarrior configuration can also be read from the file using the [file lookup plugin](https://docs.ansible.com/ansible/latest/plugins/lookup/file.html) or from a Jinja template with the [template lookup plugin](https://docs.ansible.com/ansible/latest/plugins/lookup/template.html):

```yaml
taskwarrior_configuration: "{{ lookup('file', 'my_config.conf') }}"
```

Syncing to a taskserver
-----------------------

With the following variables you provide the names of certificates which are needed for connecting to a taskserver. If those variables are set, the certificates are copied to the remote machine. Note that you want to protect them properly (e.g. with [Ansible vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html):

```yaml
taskwarrior_server_certificate: taskwarrior_server.cert.pem
taskwarrior_client_certificate: taskwarrior_client.cert.pem
taskwarrior_client_key: taskwarrior_client.key.pem
```

This role automatically sets the configuration settings `taskd.ca`, `taskd.key` and `taskd.certificate`. However you need to add the missing configuration settings for using a taskserver in the Ansible variable `taskwarrior_configuration`:

```yaml
taskwarrior_configuration: |
  taskd.server=...
  taskd.credentials=...
```

In the taskwarrior documentation you can find more information for [configuring taskwarrior with a taskserver](https://taskwarrior.org/docs/taskserver/taskwarrior.html).

Dependencies and Requirements
-----------------------------

This role has no dependencies or requirements.

License
-------

To the extent possible under law, I waive all copyright and related or neighboring rights to this software stored under [https://github.com/kulla/ansible-role-taskwarrior](https://github.com/kulla/ansible-role-taskwarrior). Thus, I publish this software under the [CC0 1.0 Universal (CC0 1.0) Public Domain Dedication](https://creativecommons.org/publicdomain/zero/1.0/deed.en). This software is published from Germany.

Author Information
------------------

[Stephan Kulla](http://kulla.me/)
