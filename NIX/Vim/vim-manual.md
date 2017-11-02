# Vim Manual

Notes from the Vim Manual, Neovim edition. Sections with basic and irrelevant content are skipped, hence odd section numbering.

## About the Manuals `usr_01.txt`

### 01.1 Two Manuals

Vim docuementation comes in two parts, The User Manual which reads like a book, and The Reference Manual which is a precise description of how Vim works. Bars can be used to jump between them.

### 01.2 Vim Installed

Neovim has an example vimrc that can be found at `$VIMRUNTIME/vimrc_example.vim`, the same as in a normal Vim distrobution. This can be copied within Neovim like so `!cp -i $VIMRUNTIME/vimrc_example.vim ~/.config/nvim/init.vim` to replace the default 'init.vim'/'.vimrc'. For more info: `:h vimrc`.

### 01.3 Using the Vim Tutor

Use the built in vimtutor with `:Tutor`, basically the same as `vimtutor` but with some modern niceties.

## The First Steps in Vim `usr_02.txt`

### 02.2    Inserting text

To be able to see what the current mode is use the command `:set showmode`, although this doesn't show normal mode is will show Insert, Replace, and Visual mode (are there other lesser known modes?).

### 02.4    Deleting characters

Deleting a line break - two lines can be joined together with the command `J`, short for join, which will remove the line break from the current line, thus joinging the line below to the current line.

### 02.6    Other editing commands

Counts can be used with all editing commands, so to remove 3 letters `3x` can be used.

Counts can also be combined when inserting text, so `5a.b` will type out `.b.b.b.b.b`, although this will only be output when switching to normal mode. This would be useful for generating patterns or a long string of text such as `----` for a markdown table. Entering will not stop it either, so a multiline pattern can easily be created.

### 02.8    Finding help

The help pages are really just a normal editing window with the file set to unmodifiable/readonly, so it can be navigated the same way.

* `ZZ` can be used to quit a help window, or `:q`.
* `C-]` to jump to a tag/bar.
* `C-t` to go back to the prior position, aka pop tag
* `C-o` to jump back to an older position

Examples help searches:

* `:h help-summary` - summary of useful help searches
* `:h index` - get a complete index of all Vim commands
* `:h x`
* `:h deleting`
* `:h CTRL-A` or `:h ^A`
* `:h -t` - find out what the `-t` command line argument does when starting Vim.
* `:h 'number'` - find out what the 'number' option does, options should be enclosed in single quotes.
* `:h E37` - get help on an error message with the error Id if the inline message isn't clear enough