# Get configuration from device
The `get_config` function will return the either the current active or current
saved configuration from an Arista EOS devices.  This function is only
supported over `network_cli` connections and must be configured to enter
`enable` mode using `ansible_become`.  

The `get_config` function will also parse the device active configuration into
a set of host facts during its execution.  All of the parsed facts are stored
in the ``arista_eos.config`` top level facts key.

## How to get the device configuration
Retrieving the configuration from the device involves just calling the
`get_config` function from the role.  By default, the `get_config` role will
return the device active (running) configuraiton.  The text configuration will
be returned as a fact for the host.  The configuration text is stored in the
`configuration` fact.

Below is an example of calling the `get_config` function from the playbook.

```
- hosts: arista_eos

  roles:
    - name ansible-network.arista_eos
      function: get_config
```

The above playbook will return the current running config from each host listed
in the `arista_eos` group in inventory.

### Get the current startup config
By default the `get_config` function will return the device running
configuration.  If you want to retrieve the device startup configuration, set
the value of `source` to `startup`.

```
- hosts: arista_eos

  roles:
    - name ansible-network.arista_eos
      function: get_config
      source: startup
```

### Implement using tasks
The `get_config` function can also be implemented in the `tasks` during the
playbook run using either the `include_role` or `import_role` modules as shown
below.

```
- hosts: arista_eos

  tasks:
    - name: collect facts from arista eos devices
      import_role:
        name: ansible-network.arista_eos
        tasks_from: get_config
```

## Arguments

### source

Defines the configuration source to return from the device.  This argument
accepts one of `running` or `startup`.  When the value is set to `running`
(default), the current active configuration is returned.  When the value is set
to `sartup`, the device saved configuration is returned.

The default value is `running`

## Notes
None
