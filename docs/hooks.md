# Hooks

Hooks are a featured provided by this role that allows playbook designers to
inject a set of tasks at various defined points in the role execution.  This is
useful when there is a need to sometimes change the behavior of a role at run
time. 

Any function that supports one or more hooks will have defined the hook name in
the function documentation.  To use a hook simply provide a variable via the
inventory or playbook that provides a path to the tasks to execute if and/or
when the hook is triggered.

For example, lets assume we want to run a set of tasks after a configuration is
is automatically rolled back due to a configuration error.  In order to do
this, we could simply define the hook as part of the function definition in the
playbook.

```
- hosts: arista_eos

  roles:
    - name: ansible-network.arista_eos
      function: load_config
      config_file: eos.cfg
      eos_configuration_rollback_post_hook: tasks/verify_neighbors.yaml
```

The the above example, the `load_config` function is called and the `eos.cfg`
file is loaded into the target device(s).  If the configuration load fails for
any reason, then the rollback is automatically invoked.  

Once the function is done installing the previous configuration, it will run
the tasks defined in `tasks/verify_neighbors.yaml`

Hooks are a powerful mechanism to allow playbooks to respond to events during
role run time execution.  The tasks provided by the hook are simply a list of
standard Ansible tasks.
