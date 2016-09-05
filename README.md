nagios4_server_plugins
=========

This role installs and could add easily more plugins and commands plugins to nagios. 

Just add the plugin to files/plugins
Then add the commands to use it to files/commands

Those will be copied automatically to right place.

Please check the actual amount of commands already delivered with plugins.
Also check templates/ with two added commands files.

Requirements
------------

It requires you have nagios4_server already setup, recommended with our ansible role.


Role Distribution support
------------------------

Ubuntu: ok
RedHat: No

Role Variables
--------------

Uses vars/{{ ansible_distribution}}.yml 
Commands are copied to {{ nagios_config_cfg_dir}}/plugins
Plugins to /usr/lib/nagios/plugins

For your hosts/groups_vars:

check_url_proxy_server: 'proxy_server'
check_url_proxy_user: 'proxy_user'
check_url_proxy_password: 'proxy_password'

Dependencies
------------

ansiblecoffee.nagios4_server

Example Playbook
----------------

### Minimum usage:

    - hosts: servers
      roles:
        - ANXS.mysql
        - nagios4_server
        - nagios4_server_plugins

### Full list of roles:

``` yaml
- name: apply Nagios settings
  hosts: nagios4_servers
  become: yes
  become_method: sudo
  roles:
    - { role: nagios4_server, tags: ["install", "nagios4_server_all", "nagios4_server"] }
    - { role: nagios4_server_plugins, tags: ["install", "nagios4_server_all", "nagios4_server_plugins"] }
    - { role: nagios4_server_pnp4nagios, tags: ["install", "nagios4_server_all", "nagios4_server_pnp4nagios"] }
    - { role: ANXS.mysql, tags: ["install", "nagios4_server_all", "nagios4_server_thruk", "ANXS.mysql"] }
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

License
-------

BSD

Author Information
------------------

Main authors: Diego Daguerre, Pablo Estigarribia.
Site: https://github.com/ansiblecoffee


