nagios4_server_plugins
======================

[![Build Status](https://travis-ci.org/CoffeeITWorks/ansible_nagios4_server_plugins.svg?branch=master)](https://travis-ci.org/CoffeeITWorks/ansible_nagios4_server_plugins)

This role installs and could add easily more plugins and commands plugins to nagios. 

Options to add plugins to your nagios: 

* Just add the plugin to files/plugins
* Edit some of the vars shown in [defaults/main.yml](defaults/main.yml) 
  * clone repositories with `nagios_plugins_repos` var.
  * Install from pip3 with `nagios_plugins_pip3_packages` var.
  * Install from pip2 with `nagios_plugins_pip2_packages` var.
  * add apt packages with `nagios_plugins_apt_packages` var.

To install wmic and wmiplus plugin and commands (Also supports Ubuntu 16.04+):

    nagios_plugins_install_checkwmiplus: True

Then add the commands to use it, edit `templates/commands/command_file.cfg`.

Or also add files in `templates/commands` dir in this role.

Those will be copied automatically to right place.

Please check the actual amount of commands already delivered with plugins.
Also check templates/ with two added commands files.

Requirements
------------

It requires you have nagios4_server already setup, recommended with our ansible role.

Role Distribution support
------------------------

Ubuntu: ok  
Debian: ok  
RedHat: No  please check tests.txt file for details.  
Ubuntu latest LTS: ok

Role Variables
--------------

Check [defaults/main.yml](defaults/main.yml) 

Commands are copied to {{ nagios_config_cfg_dir}}/plugins
Plugins to {{ nagios_plugins_dir }}

For your hosts/groups_vars:

```yaml
check_url_proxy_server: 'proxy_server'
check_url_proxy_user: 'proxy_user'
check_url_proxy_password: 'proxy_password'
```

Dependencies
------------

ansiblecoffee.nagios4_server

Example Playbook
----------------

### Minimum usage:

```yaml

- hosts: servers_nagios
  vars:
    nagios_plugins_install_checkwmiplus: True
  roles:
    - role: ansible-role-nagios
    - role: coffeeitworks.ansible_nagios4_server_config
    - role: ansible_nagios4_server_plugins
```

### Full list of roles:

See [requirements.yml](requirements.yml) for some example on names of the roles.

Most of them could be `coffeeitwork.name` instead of just name, but the example is with names simplified.

``` yaml
- name: apply Nagios settings
  hosts: nagios4_servers
  become: yes
  become_method: sudo
  roles:
    - { role: nagios4_server, tags: ["install", "nagios4_server_all", "nagios4_server"] }
    - { role: nagios4_server_plugins, tags: ["install", "nagios4_server_all", "nagios4_server_plugins"] }
    - { role: nagios4_server_pnp4nagios, tags: ["install", "nagios4_server_all", "nagios4_server_pnp4nagios"] }
    - { role: geerlingguy.mysql, tags: ["install", "nagios4_server_all", "nagios4_server_thruk", "ANXS.mysql"] }
    - { role: nagios4_server_thruk, tags: ["install", "nagios4_server_all", "nagios4_server_thruk"] }
    - { role: postfix_client, tags: ["install", "nagios4_server_all", "postfix_client"] }
# Additional tags: role/tag
# nagios4_server             - config_nagios
# nagios4_server             - nagios4_server_main_config
# nagios4_server             - config_nagios_cron
# nagios4_server_plugins     - config_nagios_plugins
# nagios4_server_plugins     - test_nagios_plugins
# nagios4_server_pnp4nagios  - test_nagios_pnp4nagios
# nagios4_server_thruk       - config_nagios_thruk_cron
# nagios4_server_thruk       - test_nagios_thruk
# nagios4_server_thruk_git   - config_nagios_thruk_git_cron
```

Tags:

    config_nagios_plugins
    test_nagios_plugins

We require some help to support centos7  

TODO: 

* add tests to use it with icinga 

License
-------

BSD

Author Information
------------------

Main authors: Diego Daguerre, Pablo Estigarribia.
Site: https://github.com/CoffeeITWorks


*end file
