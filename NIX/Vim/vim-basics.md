# Vim Basics

Notes on the basics of using Vim, as covered by the vimtutor tool.

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
* Insert text after the character the cursor is currently on with `a`.
* Insert text at the end of the current line with `A`.

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

These will have the same result be behave slightly differently, and can have subtle afteraffects relating to what is available in the copy buffer.

* `d2w` - deletes two words
* `2dd` - delete two lines, alternately `d2d` will also delete two lines, although only the second line will be 'yanked' and still be pasteable.

## The Undo Command

* `u` - undo the last command
* `U` - undo the changes to a whole line
* `C-r` - redo a command/undo an undo