# infinity's dotfiles

A simple, slimmed down, opinionated, yet flexible set of `dotfiles`.

## Inclusions

- `zsh` for shell
- `brew` for packages
- `starship` for prompt
- `fnm` for Node version management
- `rbenv` for Ruby version management
- `pyenv` for Python version management
- Optimized for macOS
- Custom theme based on Snazzy/Dracula

## Installation

To install just simply clone this repo to your home directory and run.

```shell
# Set up dotfiles path.
export DOTFILES=$HOME/.dotfiles
# Clone dotfiles locally.
git clone git@github.com:infinityrobot/dotfiles.git $DOTFILES
# Initialize!
for f in $DOTFILES/{utils,init,aliases}/*; do source $f; done
# Reload shell!
reload
```

Dotfiles and dependencies will be installed / initialized on first run if a clean machine is detected.

If you would like to include infinity's macOS settings, run `source $DOTFILES/config/macos.zsh` after installing.

## Updating

To update, just pull from `main`.

## Customization

Local customizations can be included in `~/.zshrc.local`.
