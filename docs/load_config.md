# Load configuration into device
The `load_config` function provides a means to load a configuration file onto a
target device running Arista EOS.  The `load_config` function provides
configuration values that allow the source configuration to either be merged
with the current active configuration (default) or to replace the current
active configuration on the device.  

This function also supports a rollback capability.  If the provided
configuration file fails to load during merge operations, the previous
configuraiton is automatically re-installed on the device.  

## How to load and merge a configuration
Loading a configuration onto a target device is fairly simple and
straightforward.  By default, the `load_config` function will merge the
contents of the provided configuration file with the configuration running on
the target device.  

Below is an example of how to call the `load_config` function.

```
- hosts: arista_eos
  
  roles:
    - name: ansible-network.arista_eos
      function: load_config
      config_file: eos.cfg
```

The example playbook above will simple load the contents of `eos.cfg` onto the
target network devices and merge the configurations.

## How to load and replace a configuration
The `load_config` function also provides support for replacing the current
configuration on a device.  In order to use the replace feature, the target
Arista EOS device must support configuration sessions.

In order to replace the configuration, the function as before but adds the
value `replace: yes` to the playbook to indicate that the configuration should
be replace.

Note: Take caution when doing configuration replace that you do not
inadvertantly replace your access to the device.

```
- hosts: arista_eos

  roles:
    - name ansible-network.arista_eos
      function: load_config
      config_file: eos.cfg
      replace: yes
```

## Arguments

### eos_config_replace

This value enables or disables the configuration replace feature of the
function.  In order to use `eos_config_replace` the target device must support
configure sessions.  

The default value is `False`

#### Aliases

* replace

### eos_config_file

This required value provides the path to the configuration file to load when
the function is called.  The path to the file can either be provided as
relative to the playbook root or an absolute path.  

The default value is `null`

This value is *required*

#### Aliases

* config_file

###  eos_config_session_name

The configuration session name is automatically set by the function if an
alternative one is not provided.  If you wish to provide a custom config
session name, set this value.  Typically this value does not need to be
changed.

The default value is `cfg-ansible`

### eos_config_checkpoint_filename

The name of the checkpoint file to be created on the local device is defined by
this setting and does not typically need to be changed.   The checkpoint file
is created on the default flash file system.

The default value is `tmp_ansible`

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
