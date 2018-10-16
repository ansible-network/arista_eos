===============================
arista_eos
===============================

2.6.2
=====

Major Changes
-------------

- Added configure_vlan task
- Replace eos_config_file to config_manager_file

2.6.1
=====

Major Changes
-------------

- remove set checkpoint filename in task list

Minor Changes
-------------

- Make changes in configure_user for dir structure change
- Refactored template to mitigate bugs
- updates the load function to handle the config manager
  variables correctly for loading a configuration from a file.
- Update config_manager_text into the task list to handle
  text coming from the config_manager role.
- the config_manager_replace fact to the eos_config_replace
  value to handle the config replace function.
- set the default value for eos_config_replace in
  config_manager/load to False.
- set the checkpoint file name in the load function instead of
  using the defaults/ file.  This gives load greater control of
  the checkpoint includes.
- Refactor template and modify task after dir structure change
- update includes/configure/ to detect errors in line loading
- update load_config_spec file
- update config_manager/load tasks

2.6.0
=====

New Functions
-------------

- NEW `get_facts` for collecting facts from nxos devices
- NEW `get_config` facts to return the active configuration as parsed facts
- NEW `load_config` loads configuration onto remote device
- NEW `clear_sessions` clears all configuration sessions 
- NEW `save_config` saves the current running-config to startup-config


Major Changes
-------------

- Initial release of the `arista_eos` role.
