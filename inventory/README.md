# Inventory

## Files structure

Top level YAML files contain hosts and groups definitions. They can optionally contain variables specifc to hosts and groups.

`host_vars/` directory contains files with host-specific variables. Each file inside must be named exactly like the host it keeps variables for.

`group_vars/` directory contains files with group-specific variables. Each file inside must be named exactly like the group it keeps variables for.

## Merging data structures

If the same variable names are describing the same host in top level YAML and `host_vars/`, then Ansible merges the variables according to the rules described in documentation. The same applies for `group_vars/`

As the top level YAML files may contain definitions or variables of the same hosts or groups, merging rules applies there as well.
Since the merging mechanism reads files in ASCII order, it's recommended to prefix the file names with numbers to keep kontrol of the files priorities. Keep in mind that lower number will be taken first, so if the same variable is defined in 2 files, then the variable from the file with higher number will overwrite it.

