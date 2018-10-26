# Load configuration into device
The `config_manager/load` function provides a means to load a configuration 
file onto a target device running Arista EOS.  The `config_manager/load` 
function provides configuration values that allow the source configuration 
to either be merged with the current active configuration (default) or to 
replace the current active configuration on the device.  

This function also supports a rollback capability.  If the provided
configuration file fails to load during merge operations, the previous
configuraiton is automatically re-installed on the device.  

## How to load and merge a configuration
Loading a configuration onto a target device is fairly simple and
straightforward.  By default, the `config_manager/load` function will merge the
contents of the provided configuration file with the configuration running on
the target device.  

Below is an example of how to call the `config_manager/load` function.

```
- hosts: arista_eos
  
  roles:
    - name: ansible-network.arista_eos
      function: config_manager/load
      config_manager_text: "{{ lookup('file', 'config.txt') }}"
```

The example playbook above will simple load the contents of `eos.cfg` onto the
target network devices and merge the configurations.

## How to load and replace a configuration
The `config_manager/load` function also provides support for replacing the 
current configuration on a device.  In order to use the replace feature, 
the target Arista EOS device must support configuration sessions.

In order to replace the configuration, the function as before but adds the
value `config_manager_replace: yes` to the playbook to indicate that the 
configuration should be replace.

Note: Take caution when doing configuration replace that you do not
inadvertantly replace your access to the device.

```
- hosts: arista_eos

  roles:
    - name ansible-network.arista_eos
      function: config_manager/load
      config_manager_text: "{{ lookup('file', 'config.txt') }}"
      config_manager_replace: yes
```

## Arguments

### config_manager_text

The configuration text to load into the remote device.  The value must be the
full text configuration to either merge or replace on the target host.  

The default value is `null`

### config_manager_replace

This value enables or disables the configuration replace feature of the
function.  In order to use `config_manager_replace` the target device must 
support configure sessions.  

The default value is `False`

### eos_rollback_enabled

By default, if an error is enountered while loading the configuration file, the
function will automatically reload the previous active configuration.  This
feature is enabled by default but can be disabled by setting this value to
`False`.

The default value is `True`

## Hooks

The values below provide the names of the hooks supported by this function. For
more details about hooks and how they are using see [Hooks](https://github.com/ansible-network.arista_eos/blob/devel/docs/hooks.md)

### eos_restore_checkpoint_pre_hook

This hook is executed once the checkpoint restore is triggered but before the 
checkpoint configuration is loaded into the device.

### eos_restore_checkpoint_post_hook

This hook is executed once the checkpoint configuration has been successfully
loaded into the target device but before the function exits.

## Notes
None
