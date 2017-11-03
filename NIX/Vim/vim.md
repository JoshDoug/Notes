# Vim

Using Vim.

Tutorials and useful links:

* `vimtutor` - tutorial program, Neovim has its own tutorial accessible via `:Tutor`
* [Vim Home Page](vim.org)
* [Vim FAQ on Sourceforge](vimdoc.sf.net)
* [Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/) (kinda old)
* [Learning Vim in 2014](http://benmccormick.org/learning-vim-in-2014/) (also kinda old)
* [Bram Moolenaar's Seven habits of effective text editing](http://www.moolenaar.net/habits.html)

## Vim Modes

Vim has n modes: insert mode, normal mode, replace mode?, visual mode?, what else?

## Exiting Vim

* `:q` - quit Vim if only one file is open, or close the current window if multiple windows/files are open
* `:q!` - force quit Vim even if a files changes haven't been saved
* `:qa` - quit Vim even if multiple files are open (but don't force it incase changes haven't been saved)
* `:qa!` - force quit Vim with multiple files open, any changes will be lost
* `:wq` or `ZZ` - write the current file and quit, if more than one file is open then this will save the current file and close the pane or tab.

## Scrolling

* `C-e` - scroll down a line
* `C-y` - scroll up a line
* `C-f` - scroll forward a page
* `C-b` - scroll backwards a page
* `C-d` - scrolls down half a page
* `C-u` - scrolls up half a page
* `zz` - scroll current line to the middle of the screen
* `zt` - scroll current line to the top of the screen
* `zb` - scroll current line to the bottom of the screen

Moving the cursor around:

* `H`, `M`, `L` - High, Middle, Low, move the cursor to the top, middle, and bottom of the page

## Repeat a Command: `.`

## Using Panes and Tabs/Windows

* To list the current open buffers: `:ls`
* Make the current pane the only pane visible: `:only`, useful when just checking help without any files open, to do this in one go: `:h | only`
* Open help in a new tab: `:tab h`
* To close a pane or window: `C-w c`
* To switch panes: `C-w w` or `C-w C-w`
* Switch tabs: `:tabn` or `gt` to cycle through tabs to the right, `tabp` or `gT` to cycle through tabs in reverse.

## Vim CLI

Access the CLI from normal mode by typing `:`.

* Chain commands: `:tabnew | h quickref | only` - this would open a new tab, open the quickreference help, and then make the help pane fullsize.
* Use shell commands: `:r !ls` to read the contents of `ls` into the current file
* Check Vim Environment Variables: `echo $MYVIMRC` - Vim environmnet variables are only accessibly within Vim unless they're set manually (or some other way I don't know about), another EV example is `$VIMRUNTIME`

## Vim Help

Check the vim-help.md section for more in depth notes. Two useful help pages:

* `:h help-summary` - summary of useful help searches
* `:h index` - get a complete index of all Vim commands