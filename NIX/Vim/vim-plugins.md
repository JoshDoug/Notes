# Vim Plugins

Vim has a wealth of plugins and several plugin managers to manage them with.

## Plugin Managers

* [NeoBundle](https://github.com/Shougo/neobundle.vim) - no longer actively developed, just bug fixes, specifies Vim/Neovim support
* [Dein.vim](https://github.com/Shougo/dein.vim) - recommended replacement for NeoBundle, specifies Vim/Neovim support
* [Vundle](https://github.com/VundleVim/Vundle.vim) - most popular plugin manager by GitHub stars
* [vim-plug](https://github.com/junegunn/vim-plug) - minimalist Vim plugin manager, specifies NeoVim support
* [VAM - Vim Addon Manager](https://github.com/MarcWeber/vim-addon-manager) - least popular by GitHub starts, but seems well maintained & responsive to issues
* [Pathogen](https://github.com/tpope/vim-pathogen) - Tim Pope, guy who maintaines Vim
* Vim 8 (and Neovim?) have some built in plugin/package management support.

## vim-plug

Setup with Neovim:

* `curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim`
* Add following to top of .vimrc/init.vim, vim-airline is an example plugin:

```vim
call plug#begin('~/.local/share/nvim/plugged')

Plug 'vim-airline/vim-airline'

call plug#end()
```

* Restart vim or source the vimrc `:source ~/.config/nvim/init.vim`
* Run `:PlugInstall`, `PlugUpdate`, `PlugUpgrade` to ensure plugins are installed, updated, and then vim-plug itself is updated.