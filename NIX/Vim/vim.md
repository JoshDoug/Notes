# Vim

Using Vim.

Tutorials and useful links:

* vimtutor

## Vim Modes

Vim has n modes: insert mode, normal mode, replace mode?, visual mode?, what else?

## Exiting Vim

* `:q` - quit Vim if only one file is open, or close the current window if multiple windows/files are open
* `:q!` - force quit Vim even if a files changes haven't been saved
* `:qa` - quit Vim even if multiple files are open (but don't force it incase changes haven't been saved)
* `:qa!` - force quit Vim with multiple files open, any changes will be lost

## Using Vim Help

## Using Panes and Tabs/Windows

* To list the current open buffers: `:ls`
* Make the current pane the only pane visible: `:only`, useful when just checking help without any files open, to do this in one go: `:h | only`
* Open help in a new tab: `:tab h`