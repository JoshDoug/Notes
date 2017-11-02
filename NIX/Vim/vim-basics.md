# Vim Basics

Notes on the basics of using Vim, as covered by the vimtutor tool and Neovim `:Tutor`.

## Moving the Cursor

Basic cursor navigation:

* `h` - move left one character
* `j` - move down one line
* `k` - move up one line
* `l` - move right one character
* Arrow keys also work

Holding down the key will make it repeat.

## Exiting Vim and Saving Files

Exiting Vim, everyone's favourite joke (although I found exiting Emacs harder?!)

1. Switch to normal mode, either with the `<ESC>` key, or anything rebound to `<ESC>` such as `jj` in my dotfiles
2. Quit: `:q`, or to force quit: `:q!`

Saving edits: switch to normal mode, enter `:w`, this will write the fill out, setting the changes and saving it. These commands can be combined to save a file and quit vim: `:wq`.

## Text Editing - Deletion, Insertion, Appending

* Remove a character by navigating the cursor to it and typing `x`.
* Insert text by pressing `i` at the point where text is to be inserted, this will insert it before the character the cursor is currently on.
* Insert at the beginning of the current line with `I`.
* Append text after the character the cursor is currently on with `a`.
* Append text at the end of the current line with `A`.
* Open a new line below the cursor with `o`.
* Open a new line above the cursor with `O`.

## Deletion Commands

* `dw` - delete until the start of the next word
* `d$` - delete from the cursor to the end of the line, including the character the cursor is on
* `dd` - delete the current line

## Operators and Motions

Many commands that chanage text are made from an operator and a motion. So a delete commands would be: `d motion`.

Where:

* `d` is the delete operator
* `motion` is what the operator will operate on

A short list of example motions:

* `w` - until the start of the next word
* `e` - to the end of the word, this will not affect whitespace
* `$` - to the end of the line

Pressing just the motion without an operator will move the cursor as described, so `e` will move to the end of a word.

## Using a Count for a Motion

Typing a number before a motion will repeat it that many times, examples:

* `2w` - will move forward two words
* `0` - move to the start of the line
* `5j` - will move down 5 lines

## Using a Count with an Operator and Motion

A count, operator, and motion can be combined.

* `operator count motion`
* `count operator motion`

These will have the same result be behave slightly differently, and can have subtle afteraffects relating to what is available in the copy buffer/register.

* `d2w` - deletes two words
* `2dd` - delete two lines, alternately `d2d` will also delete two lines, although only the second line will be 'yanked' and still be pasteable.

## The Undo Command

* `u` - undo the last command
* `U` - undo the changes to a whole line
* `C-r` - redo a command/undo an undo

## The Put Command

I don't know why this isn't just called the paste command. Type `p` to put previously deleted or yanked text after the cursor.

* `p` - this will put the text after the cursor, if it's an entire line it will put it on the line below
* `P` - this will put the text before the cursor, if it's an entire line it will put it on the line above

## The Replace Command

Replace a character with the `r` operator followed by the character to replace it with.

* `rx` will replace the current character the cursor is on with x.
* `R` switches into replace mode and will overwrite characters until returning to normal mode. Replace mode is like Insert mode except every typed character deletes an existing character. Using the backspace/delete key over replaced text will undo the replacement.

## The Change Operator

The change operator is `c`, which can be combined with motions to change a word, line, etc. It's basically the same as the delete operator but automatically switches to insert as well.

## Cursor Location and File Status

* `C-g` - shows the current line number of the cursor along with the filename at the bottom of the page.
* `G` - move to the last line of the file
* `gg` - move to the first line of the file
* `489G` - move to line 489 in the file

## The Search Command

* Type `/` followed by the phrase to find, the `/` will appear at the end of the file with the cursor along with any text that's typed.
* Hit enter to find the first instance of the text after the cursor.
* To move to the next instance of a phrase type `n`, to move to a prior instance type `N`.
* To search for a phrase in the reverse direction use `?` instead of `/`.
* To go back to where the cursor was during the search: `C-o`, while `C-i` goes forward.
* To ignore case for a specific search add `\c` to the end of the search, e.g. `/testsearch\c`

## Matching Parentheses Search

Type `%` while on a bracket to move to the matching bracket, this works for parentheses, brackets, and curly braces. Handy for jumping a code block or finding mismatched brackets.

## The Substitue Command

* `:s/old/new` - change the first occurrence of the word old on the current line to new.
* `:s/old/new/g` - change all occurrences of the world old on the current line to new, g means change globally within the line.
* `:s/old/new/gc` - change all occurrences of the world old on the current line to new, with a prompt asking whether or not to make the change, `c` stands for confirmation.
* `:%s/old/new/g` - change every occurrence within the file
* `:%s/old/new/gc` - change every occurrence in the file with a prompt on whether to make the change or not
* `#,#s/old/new/g` - change every occurrence between the line numbers, where `#,#` are the line numbers.

## Execute an External Command

Type `:!` followed by an external command and `<ENTER>` to execute that command, e.g. `:!ls`, this allows the running of shell commands. Commands can also take options and arguments like normal, but importantly aliases will not work.

Examples:

* `:w testfile` - this writes out the current file to testfile
* `:!rm testfile` - remove the testfile created previously, tab complete would work for completing the filename here

## Selecting Text to Write

Select text to save to another file: `v motion :w Filename`

1. Use `v` to enter Visual Mode, then navigating with the cursor will highlight the seleced text from that point.
2. Typing `:` will cause `:'<,'>` to appear at the prompt.
3. Type `w TEST` at the prompt after the other characters to write out the hightlighted portion to the file TEST.
4. The full prompt should look like this before the command is entered: `:'<,'>w TEST`

To toggle Visual Mode off type `v` again, to cancel.

## Retrieving and Merging Files

To insert the contents of a file (not sure how often this is useful) use: `:r filename`, the file will be inserted on a new line below the cursor. The `r` command is short for retrieve. This command will also work with shell commands, so `:r !ls` will insert the output of `ls`.

## Copy and Paste Text

Use `y`, yank, and `p`, paste to copy and paste text. Text can be copied with visual mode, or used as an operator with counts and motions.

* In visual mode select the text to be copied and then type `y` to yank it.
* In normal mode `y` can be used as an operator, copy a word with `yw`, a line with `yy`, two lines with `2yy` or `y2y`

Pasting has already been covered by the Put command above.

## Set Option

Options can be set via the CLI that last for the duration of the Vim session:

* `:set ic` - sets Vim to ignore case while searching using `/`
* `:set noic` - sets Vim to ignore case while searching
* `:set hls is` - sets the `hlsearch` and `incsearch` options using their shorthands
* `:set nohlsearch` - turns of search highlighting
* To switch an option off use the same set command but prepend the feature name with 'no', e.g. `:set nois` to turn off incremental search
* The Neovim tutorial mentions prepending an option with `inv` to toggle it, e.g. `:set invic`, 'inv' is presumably short for invert.

## Getting Help

To get help in Vim use `:help`, this will open the main help menu which explains how to use it.

To get help with something more specific add the search term after the help command: `:help w` to get help on writing to a file. Other examples:

* `:help c_CTRL-D`
* `:help insert-index`
* `:help user-manual`

Use `C-w C-w` to jump from one window to another and `:q` to quit help.

## Create a Startup Script

Enable Vim Features with a startup script. An example vimrc file is at `$VIMRUNTIME/vimrc_example.vim` and vimrc help can be found using `:help vimrc-intro`.

The location of the starup script can be found from within Vim using the command: `:echo $MYVIMRC`. When using Neovim for example, the fie is at `~/.config/nvim/init.vim`, although this file also sources a normal .vimrc in my home directory.

## Completion

Command line completion with `C-d` and `<TAB>`.

1. Set Vim to 'not compatible' mode with `:set nocp`, this breaks compatibility with Vi.
2. Type the start of a command, e.g. `:e` and press `C-d`, this will show a list of the possible commands that start with 'e', these can then cycled through by tabbing.
3. Now that `:edit` has been entered `C-d` can be used to list files (although there needs to be a space after the edit command) and tab complete can be used as well.