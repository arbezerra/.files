# .files

Configuration files.

Each application owns a repository-local directory containing only its actual
configuration. Target-specific paths such as `.config/` and `.local/` live only
in the Ansible symlink map, not in the source tree.

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
- `ansible/inventory/group_vars/all/main.yml`: package and user configuration
- `ansible/inventory/group_vars/all/symlinks.yml`: dotfile symlink map
- `ansible/roles/`: install and configuration roles

For example, `kitty/kitty.conf` is linked to `~/.config/kitty/kitty.conf`, and
`zsh/.zshrc` is linked to `~/.zshrc`.

Thanks prime for his [.dotfiles](https://github.com/ThePrimeagen/.dotfiles)
