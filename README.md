nsswitch
========

Role which helps to manage the nsswitch.conf file.


Example
-------

```
---

# Default usage
- hosts: myhost1
  roles:
    - nsswitch

# Example of how to add a new option to a database
- hosts: myhost2
  vars:
    # Add 'sss' option to the groups database
    nsswitch_group:
      - files
      - sss
  roles:
    - nsswitch

# Example of how to suppress some of the database
- hosts: myhost3
  vars:
    # Set value to empty list to suppress a database
    nsswitch_bootparams: []
  roles:
    - nsswitch

# Example of how to add an additional database
- hosts: myhost4
  vars:
    # Definition of the new database
    my_nsswitch_customdb:
      customdb:
        - files
    # Add the custom database by updating it with the default database
    my_nsswitch_config: "{{
      my_nsswitch_customdb.update(nsswitch__all)
    }}{{ my_nsswitch_customdb }}"
  roles:
    - role: nsswitch
      nsswitch_config: "{{ my_nsswitch_config }}"

# Example of how to redefine the configturation from scratch
- hosts: myhost5
  vars:
    # The new nsswitch config will contain only passwd, shadow, group and
    # hosts databases
    nsswitch_config:
      passwd:
        - files
      shadow:
        - files
      group:
        - files
      hosts:
        - files
  roles:
    - nsswitch
```


Role variables
--------------

List of variables used by the role:

```
# Default location of the config file
nsswitch_file_location: /etc/nsswitch.conf

# Aliases
nsswitch_aliases:
  - files
  - nisplus

# Automount
nsswitch_automount:
  - files
  - nisplus

# Bootparams
nsswitch_bootparams:
  - nisplus
  - '[NOTFOUND=return]'
  - files

# Ethers
nsswitch_ethers:
  - files

# Group
nsswitch_group:
  - files

# Hosts
nsswitch_hosts:
  - files
  - dns

# Init groups
nsswitch_initgroups:
  - files

# Net groups
nsswitch_netgroup:
  - nisplus

# Netmasks
nsswitch_netmasks:
  - files

# Networks
nsswitch_networks:
  - files

# Passwd
nsswitch_passwd:
  - files

# Protocols
nsswitch_protocols:
  - files

# Publickey
nsswitch_publickey:
  - nisplus

# RPC
nsswitch_rpc:
  - files

# Services
nsswitch_services:
  - files

# Shadow
nsswitch_shadow:
  - files

# List of all databases
nsswitch__all:
  aliases: "{{ nsswitch_aliases }}"
  automount: "{{ nsswitch_automount }}"
  bootparams: "{{ nsswitch_bootparams }}"
  ethers: "{{ nsswitch_ethers }}"
  group: "{{ nsswitch_group }}"
  hosts: "{{ nsswitch_hosts }}"
  initgroups: "{{ nsswitch_initgroups }}"
  netgroup: "{{ nsswitch_netgroup }}"
  netmasks: "{{ nsswitch_netmasks }}"
  networks: "{{ nsswitch_networks }}"
  passwd: "{{ nsswitch_passwd }}"
  protocols: "{{ nsswitch_protocols }}"
  publickey: "{{ nsswitch_publickey }}"
  rpc: "{{ nsswitch_rpc }}"
  services: "{{ nsswitch_services }}"
  shadow: "{{ nsswitch_shadow }}"

# Final configuration
nsswitch_config: "{{ nsswitch__all }}"
```


License
-------

MIT


Author
------

Jiri Tyr
