Ansible Role: oracle-gatherinfo-listener
========================================

This role automatically discovers Oracle Listeners (both standalone and registered in Grid Infrastructure).

Collected information is stored in role's `oracle_gatherinfo_listener_registered_listeners` and `oracle_gatherinfo_listener_running_listeners` variables and global `oracle_registered_listeners` and `oracle_running_listeners` variables.

Sample output:

    "oracle_registered_listeners": [
        {
            "listener_name": "LISTENER",
            "oracle_home": "/u01/app/12.1.0/grid",
            "port": "1521",
            "state": "ONLINE"
        }
    ]
    
    "oracle_running_listeners": [
        {
            "listener_name": "LISTENER",
            "oracle_home": "/u01/app/12.1.0/grid",
            "tns_admin": "/u01/app/12.1.0/grid/network/admin/"
        }
    ]


Supported OS:
-------------
* RedHat
* CentOS
* OracleLinux

Requirements
------------

This role uses `oracle` role.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):


    # collect data about Oracle listeners registered in GI OHAS
    oracle_gatherinfo_listener_from_gi_registry: true

    # List describing Oracle listeners registered in GI OHAS - Oracle High Availability Services (dynamically populated)
    oracle_gatherinfo_listener_registered_listeners: []

    # e.g.:
    #oracle_gatherinfo_listener_registered_listeners:
    #  listener_name: "LISTENER"
    #  oracle_home: "/u01/app/12.1.0/grid"
    #  port: "1521"
    #  state: "ONLINE"

    # collect data about active/running Oracle listeners
    oracle_gatherinfo_listener_running: true

    # List describing active/running Oracle listeners
    oracle_gatherinfo_listener_running_listeners: []

    # e.g.:
    #oracle_gatherinfo_listener_running_listeners:
    #  listener_name: "LISTENER"
    #  oracle_home: "/u01/app/12.1.0/grid"
    #  tns_admin: "/u01/app/12.1.0/grid/network/admin/"

    # print collected information about Oracle listeners
    oracle_gatherinfo_listener_print_collected_data: true


Dependencies
------------

This role uses `oracle` role.

Example Playbook
----------------

    - name: Gather information about installed Oracle components
      hosts: ora-servers
      gather_facts: true
      become: true
      become_user: '{{ oracle_user }}'

      tasks:

      - import_role:
          name: oracle-gatherinfo-listener
        tags:
          - oracle-gatherinfo-listener
          - oracle-gatherinfo-allcomponents	  


Inside `vars/main.yml` or `group_vars/..` or `host_vars/..`:

    #------------------------------------------------------
    # overrides role 'oracle-gatherinfo-listener' variables
    #------------------------------------------------------

    # collect data about Oracle listeners registered in GI OHAS
    oracle_gatherinfo_listener_from_gi_registry: false

    # ... etc ...


License
-------

GPLv3 - GNU General Public License v3.0

Author Information
------------------

This role was created in 2018 by [Krzysztof Lewandowski](mailto:Krzysztof.Lewandowski@fastmail.fm).

