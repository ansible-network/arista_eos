# Get facts from device
The `get_facts` function can be used to collect facts from an Arista EOS
devices.  This function is only supported over `network_cli` connection
type and requires the `ansible_network_os` value set to `eos`.

## How to get facts from the device
To collect facts from the device, simply include this function in the playbook
using either the `roles` directive or the `tasks` directive.  If no other
options are provided, then all of the available facts will be collected for the
device.

Below is an example of how to use the `roles` directive to collect all facts
from the EOS device.

```
- hosts: arista_eos

  roles:
    - name ansible-network.arista_eos
      function: get_facts
```

The above playbook will return the facts for the host under the `arista_eos`
top level key.  

### Filter the subset of facts returned
By default all available facts will be returned by the `get_facts` function.
If you only want to return a subset of the facts, you can specify the `subset`
variable and set one or more sub keys to return.  

For instance, the below will return only `interfaces` and `system` facts.

```
- hosts: arista_eos

  roles:
    - name ansible-network.arista_eos
      function: get_facts
      subset: 
        - interfaces
        - system
```

### Implement using tasks
The `get_facts` function can also be implemented using the `tasks` directive
instead of the `roles` directive.  By using the `tasks` directive, you can
control when the fact collection is run. 

Below is an example of how to use the `get_facts` function with `tasks`.

```
- hosts: arista_eos

  tasks:
    - name: collect facts from arista eos devices
      import_role:
        name: ansible-network.arista_eos
        tasks_from: get_facts
      vars:
        subset:
          - system
          - interfaces
```

## Arguments

### subset 

Defines the subset of facts to collection when the `get_facts` function is
called.  This value must be a list value and contain only the sub keys for the
facts you wish to return.

The default value is `all`

#### Current supported values for subset are
- system
- interfaces
- vlans
- switchports
- ip_interfaces
- lldp

## Notes
None


