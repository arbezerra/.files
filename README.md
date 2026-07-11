# .files

Configuration files.

## Install

This repo is managed by Ansible and targets the local machine.

```sh
./run
```

The playbook keeps the `DOTFILES` environment override:

```sh
DOTFILES="$HOME/.files" ./run
```

Ansible files live in `ansible/`:

- `ansible/playbooks/workstation.yml`: local workstation playbook
- `ansible/inventory/hosts.ini`: local inventory
- `ansible/group_vars/all/main.yml`: package and user configuration
- `ansible/group_vars/all/symlinks.yml`: dotfile symlink map
- `ansible/roles/`: install and configuration roles

Thanks prime for his [.dotfiles](https://github.com/ThePrimeagen/.dotfiles)
