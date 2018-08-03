# arista_eos

This Ansible Network role provides a set of network functions that are designed
to work with Arista EOS network devices.  The functions included in this role
include gathering facts from EOS devices, performing declarative configuration
tasks and handling various operational tasks on the device.  

## Requirements

* Ansible 2.5 or later
* Ansible Network Engine Role 2.6.2 or later

## Functions

This section provides a list of the availabe functions that are including
in this role.  Any of the provided functions can be implemented in Ansible
playbooks to perform automation activities on Arista EOS devices.

Please see the documentation link for each function for details on how to use
the function in an Ansible playbook.

* clear_sessions [[source]](https://github.com/ansible-network/arista_eos/blob/devel/tasks/clear_sessions.yaml) [[docs]](https://github.com/ansible-network/arista_eos/blob/devel/docs/clear_sessions.md)
* get_facts [[source]](https://github.com/ansible-network/arista_eos/blob/devel/tasks/get_facts.yaml) [[docs]](https://github.com/ansible-network/arista_eos/blob/devel/docs/get_facts.md)
* get_config [[source]](https://github.com/ansible-network/arista_eos/blob/devel/tasks/get_config.yaml) [[docs]](https://github.com/ansible-network/arista_eos/blob/devel/docs/get_config.md)
* load_config [[source]](https://github.com/ansible-network/arista_eos/blob/devel/tasks/load_config.yaml) [[docs]](https://github.com/ansible-network/arista_eos/blob/devel/docs/load_config.md)
* save_config [[source]](https://github.com/ansible-network/arista_eos/blob/devel/tasks/save_config.yaml) [[docs]](https://github.com/ansible-network/arista_eos/blob/devel/docs/save_config.md)

## License

GPLv3

## Author Information

Ansible Network Community (ansible-network)
