WSUS Server
=========

This role installs and configures the WSUS role for Windows 2016, and Windows 2019.

Requirements
------------

There are no special requirements apart from the standard items to allow Ansible to run on the target.

Role Variables
--------------

The following variables are defined in `/defaults/main.yml`:
* `wsus_install_management_tools`: Whether to install the WSUS MMC or not.  Default is `yes`
* `wsus_content_folder`: Sets the folder location for WSUS to store its content.  Default is `C:\WSUS`
* `wsus_products_list`: A list of products which updates will be downloaded for. Default items are `Windows Server 2016` and `Windows Server 2019`
* `wsus_classifications_list`: A list of the Update Classifications that will be enabled. Default items are `Critical Updates` and `Security Updates`
* `wsus_use_proxy`: Used to determine if proxy for WSUS Server will be configured. Default is `no`, only applies if `wsus_port` and `wsus_proxy` are defined.
* `wsus_enable_default_approval_rule`: Enable or disable the default approval rule in WSUS. Default is `true`.
* `wsus_category_sync_timeout_minutes`: Sets the amount of time in minutes for sync timeout to occur.  Default is `1000`.
* `wsus_languages`: A list of languages for which updates will be downloaded by WSUS. Default is just `en` (English)
* `wsus_choclatey_source`: Defaults to default community chocolatey repository. Default is `http://chocolatey.org/api/v2`.
* `wsus_remove_default_website`: Choice to remove default iis website.  Default is `true`.
* `wsus_install_report_viewer`: Choice on whether to install report viewer. Defaults is `True`.
* `wsus_computer_target_group_list`: List of target groups to create on WSUS Server. Defaults are `Servers` and `WorkStations`
* `wsus_targeting_mode`: Option of how to set Target Groups valid options are `Server` and `Client`
  wsus_sync_daily_time:
    hour: 0
    minute: 0
  ```
  Set the time of day when WSUS will run an automatic synchronization. Use `hour: 0` for midnight.
 
The Following variables are defined in `/vars/main.yml`:
* `wsus_script_folder`: Sets the folder for storing WSUS scripts. Default is `C:\WSUS\Scripts\`
* `wsus_log_folder`: Sets the folder for logging WSUS related items. Default is `C:\WSUS\Logs`
* `wsus_facts`: Determines whether WSUS facts should be returned

Dependencies
------------

There are no known dependencies.

Example Playbook
----------------

An example playbook for using this role:
```
  ---
  - hosts: all
    vars:
      ansible_user: 'administrator'
      ansible_become_user: System
      ansible_become_method: runas
      ansible_shell_type: powershell
      ansible_host_key_checking: False
      ansible_ssh_common_args: '-C -o ControlMaster=auto -o   ControlPersi
  st=180s -o StrictHostKeyChecking=no -o UserKnownHostsFile=/ dev/null'
      wait_for_sync: True
    roles:
      - wsus
```

License
-------

MIT

Author Information
------------------

@gamthis (Larry Lane)
