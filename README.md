# .files

Personal workstation configuration managed with Ansible. The playbook supports
Arch Linux, Debian, and Ubuntu, and is intended to run locally with sudo access.

Each application owns a repository-local directory containing only its actual
configuration. Target-specific paths such as `.config/` and `.local/` live only
in the Ansible symlink map, not in the source tree.

## Install

This repo is managed by Ansible and targets the local machine.

```sh
./run
```

The playbook installs command-line tools, desktop applications, Docker, Node.js,
Poetry, uv, Neovim, Oh My Zsh, Powerlevel10k, and the terminal font used by the
included Kitty and Alacritty configurations. It also creates the workspace
directories listed in `ansible/inventory/group_vars/all/main.yml` and changes the
login shell to Zsh.

Existing files or directories at managed destinations are preserved beside the
original path with a `.bak-<timestamp>` suffix before their symlinks are created.
Review those backups after the first successful installation and remove them when
they are no longer needed.

The playbook keeps the `DOTFILES` environment override:

```sh
DOTFILES="$HOME/.files" ./run
```

To preview changes without applying them, use Ansible check mode:

```sh
./run --check --diff
```

Check mode cannot perfectly predict commands that depend on software installed
earlier in the same run, so review its output before using it as a complete
installation test.

Ansible files live in `ansible/`:

- `ansible/playbooks/workstation.yml`: local workstation playbook
- `ansible/inventory/hosts.ini`: local inventory
- `ansible/inventory/group_vars/all/main.yml`: package and user configuration
- `ansible/inventory/group_vars/all/symlinks.yml`: dotfile symlink map
- `ansible/roles/`: install and configuration roles

For example, `kitty/kitty.conf` is linked to `~/.config/kitty/kitty.conf`, and
`zsh/.zshrc` is linked to `~/.zshrc`.

After Docker group membership is added, log out and back in before running Docker
without sudo. If the playbook reports unavailable networking modules, reboot into
the installed kernel and rerun `./run`.

Thanks prime for his [.dotfiles](https://github.com/ThePrimeagen/.dotfiles)
