# Exports.
export DOTFILES=$HOME/.dotfiles

# Source utils, initializers and aliases.
for f in $DOTFILES/{utils,init,aliases}/*; do source $f; done

# Load local zshrc.
source $HOME/.zshrc.local

# Load .zshrc from init directory if not home.
if [[ $PWD != $HOME && -f ".zshrc" ]]; then source ".zshrc"; fi
