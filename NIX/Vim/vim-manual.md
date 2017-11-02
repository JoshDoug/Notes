# Vim Manual

Notes from the Vim Manual, Neovim edition.

## About the Manuals `usr_01.txt`

### 01.1 Two Manuals

Vim docuementation comes in two parts, The User Manual which reads like a book, and The Reference Manual which is a precise description of how Vim works. Bars can be used to jump between them.

### 01.2 Vim Installed

Neovim has an example vimrc that can be found at `$VIMRUNTIME/vimrc_example.vim`, the same as in a normal Vim distrobution. This can be copied within Neovim like so `!cp -i $VIMRUNTIME/vimrc_example.vim ~/.config/nvim/init.vim` to replace the default 'init.vim'/'.vimrc'. For more info: `:h vimrc`.

### 01.3 Using the Vim Tutor

Use the built in vimtutor with `:Tutor`, basically the same as `vimtutor` but with some modern niceties.