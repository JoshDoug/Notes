# Vim Manual

Notes from the Vim Manual, Neovim edition. Sections with basic and irrelevant content are skipped, hence odd section numbering.

## 01 About the Manuals `usr_01.txt`

### 01.1 Two Manuals

Vim docuementation comes in two parts, The User Manual which reads like a book, and The Reference Manual which is a precise description of how Vim works. Bars can be used to jump between them.

### 01.2 Vim Installed

Neovim has an example vimrc that can be found at `$VIMRUNTIME/vimrc_example.vim`, the same as in a normal Vim distrobution. This can be copied within Neovim like so `!cp -i $VIMRUNTIME/vimrc_example.vim ~/.config/nvim/init.vim` to replace the default 'init.vim'/'.vimrc'. For more info: `:h vimrc`.

### 01.3 Using the Vim Tutor

Use the built in vimtutor with `:Tutor`, basically the same as `vimtutor` but with some modern niceties.

## 02 The First Steps in Vim `usr_02.txt`

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

* `:h help-summary` - summary of useful help searches, worth revisiting
* `:h index` - get a complete index of all Vim commands
* `:h x`
* `:h deleting`
* `:h CTRL-A` or `:h ^A`
* `:h -t` - find out what the `-t` command line argument does when starting Vim.
* `:h 'number'` - find out what the 'number' option does, options should be enclosed in single quotes.
* `:h E37` - get help on an error message with the error Id if the inline message isn't clear enough

## 03 Moving Around

### 03.1 Word Movement

Words in vim are just consecutive alphanumeric characters, so a word will end at a non-word character such as full stops, dashes, spaces, brackets. The `iskeyword` option can be used to change what Vim considers a word.

* `w` moves forward a word, to the start of the next word, `3w` moves three words forward
* `b` moves backwards a word, to the start of the previous word
* `e` mvoes to the end of the current word, or if already at the end of a word then to the end of the next word
* `ge` mvoes to the end of the previous word

To move by whitespace seperated words (and ignore punctuation) use uppercase motions:

* `W`
* `B`
* `E`
* `gE`

### 03.2 Moving to the Start or End of a Line

* `0` moves to the first column/character of a line (cannot take a count)
* `^` moves to the first non-whitespace/blank character of a line, useful when navigating indents (counts do nothing)
* `$` moves to the end of a line (can take a count)

### 03.3 Moving to a Character

The single-character search command is `f`, which combined with another character, and optionally a count, will search for that character within the current line to the right of the cursor. To reverse the search use `F` to search to the left of the cursor. The command `f` is short for 'find'. A similar command is the `t` command, short for 'to' which works the same but stops a character before the specified letter, similarly the reverse is `T`. These commands can be repeated with `;`, and to reverse the direction `,`. Repeating the command will not move onto another line.

The find command can be combined with other commands, e.g. `dfn` this would delete from the cursor to the first n in the current line.

### 03.4 Matching a Parenthesis

The `%` switches to the corresponding bracket/brace/parenthesis, this can be configured with the 'matchpairs' option.

### 03.5 Moving to a Specific Line

Moving lines can be done with `G`, `gg`, and e.g. `33G` to move to line 33 of a file. Or counts can be used with `j` and `k` for relative line movement.

Another way to move to a line is using the `%` command with a count to move a percentage part of a file, e.g. to move to the halfway point of a file use `50%`.

Finally to move within the current visible page `H`, `M`, and `L` can be used to move to the top, middle, and bottom of the currently visible portion of a file.

### 03.6 Telling Where You Are

To tell the current position within a file use `C-g`, alternatively with the 'ruler' option on this info will be in the bar at the bottom of the page. This bar will show the line and column position, if the number for the current column is hyphenated then it's showing the current character position of the cursor and the screen column, so if there's a tab that's a single character, but it's multiple screen columns.

Additional options set to add info about current position within a file are:

* `set number` - set absolute line numbers
* `set relativenumber` - set relative line numbers
* `set relativenumber number` - when combined the current line has an absolute number while the rest are relative
* `set ruler` - add info on current line and column at the bottom left of the status bar

### 03.7 Scrolling Around

* `C-u` - scrolls up half a page
* `C-d` - scrolls down half a page
* `C-e` - scroll down a line
* `C-y` - scroll up a line
* `C-f` - scroll forward a page
* `C-b` - scroll backwards a page
* `zz` - scroll current line to the middle of the screen
* `zt` - scroll current line to the top of the screen
* `zb` - scroll current line to the bottom of the screen

For more scrolling options check the help with `Q_sc`, and to always keep a few lines of context around the cursor use the 'scrolloff' option, for horzintal scrolling use 'sidescrolloff'.

### 03.8 Simple Searches

To search for a string use the `/` command. The characters `.*[]^%/\?~$` have special meanings, to use them in a search without the special features they need to be escaped with `\`. When searching `n` and `N` can be used to move forward and backward through the findings, and these can also take a count, so `3n` will move forward three results.

The 'ignorecase' setting can be used to ignore case when doing simple searches.

Search history can be access with the arrow keys, up arrow key goes to prior searches much like when using bash. If you start typing a command and then press up it will reduce the history to searches that match it.

NOTE: Commands using `:` also have a history, and can be accessed the same way, although the historys are seperate.

If there's a word in the text the next instance of it can be found by using `*` instead of typing it out into the search, with the cursor on the word use `*` and the search term will be automatically grabbed and inserted as the search string and the cursor will be moved to the next instance, `n` and `N` can also be used to navigate back and forth. To find the prior instance of a word use `#` which reverses the search like `?`. Importantly this doesn't just quickly add a word to the search but also moves the cursor to the next result. Counts can also be used, so `3*` will move to the 3rd occurrence of the word.

Specifying the start and the end of a word can be done with special markers, `\<` marks the start of a word and `\>` marks the end of a word.
When using `*` and `#` this is done automatically, to match partial words prefix with `g`, so `g*` and `g#`. Counts can be used like so: `3g*`, but `g3*` will not work.

Settings used with search:

* `hlsearch`, turn on: `:set hlsearch`, turn off: `:set nohlsearch`
* `:nohlsearch` can be used to turn highlighting off for the current search if it's annoying because it sticks around, this doesn't turn it off like `:set nohlsearch` does.
* `:set nowrapscan` this stops the search wrapping around to the start of the file
* `:set noincsearch` this stops incremental search results being hightlighted as the search is typed out

### 03.9 Simple Search Patterns

Vim uses regular expressions, regex, to specify what to search for, here are the essentials:

* `^` matches the start of a line, and can be used like so: `/^the`
* `$` matches the end of a line, and can be used like so: `/the$`
* Whitespace matters, so a line with an indent and then 'the' will not be matched by `/^the`
* `.` matches any single character
* Matching special characters, e.g. a full stop: `end\.` would match 'end.'.

### 03.10 Using Marks

When jumping to a position in vim with the `G` command, Vim remembers the position jumped from with a mark, this position is called a mark. To go back to that position use ``` `` ```, unfortunately this conflicts with a popular choice of tmux leader key binding, so with my config the backtick needs to be typed four times to invoke it twice within Vim. Alternatively a single quote works similarly, although not exactly the same, it will jump to the same line but to the start of the line, not the same position within the line.

* ``` `` ``` - jump to previous position (line and column), used again it will move back to where it jumped from, so it can be used to jump back and forth between two points.
* `''` - jump to previous line, but to the start of the line, and can be used to jump back and forth between two lines
* `C-o` - jump to an older point, these can move further back and aren't restricted to the two most recent points.
* `C-i` - jump to a newer point, hint `i` is next to `o` on the keyboard.
* `<TAB>` - works the same way as `C-i`

Many movements between different lines are considered a 'jump', such as searches and using `n`, but commands such as `f` or `j` do not count.

Jumps can be listed with the command: `:jumps`

#### Named Marks

Marks can be set in the text, e.g. the command `ma` would mark the current cursor point as mark a, and to get back to it just type ``` ` ``` `a`. Single quotes will also work but will go to the start of the line. Marks can be set with the letters a-z allowing for 26 possible marks. Of course `''` can still be used to jump between the two most recent marks.

To list the current marks use `:marks`, this will include marks manually set as well as current jumps.

Special marks:

* `'` - the cursor position before doing a jump
* `"` - the cursor position when last editing the file
* `[` - start of the last change
* `]` - end of the last change

## 04 Making Small Changes `user_04.txt`

### 04.1 Operators and Motions

* `d` is the delete operator
* `dw` deletes a word, starting from the point of the cursor within the word to the start of the next word
* `d3w` use a count to delete multiple words, here 3 words would be deleted
* `de` delete to the end of a word, this works like `dw` but leaves the space at the end of the word
* `d$` delete to the end of the line, including the character the cursor is on

Whether the character under the cursor is deleted depends on the command, `d$` for example is inclusive and will delete the character.

### 04.2 Changing Text

The change operator, `c`, works the same as the `d` operator except vim switches to insert mode after. Another difference is when `cw` is used the space after the word isn't deleted.

* `cc` - change a whole line, but leaves the indent intact
* `c$` - delete to the end of the line and append, basically the same as `d$a`

Shortcuts:

* `x`  stands for  dl  (delete character under the cursor)
* `X`  stands for  dh  (delete character left of the cursor)
* `D`  stands for  d$  (delete to end of the line)
* `C`  stands for  c$  (change to end of the line)
* `s`  stands for  cl  (change one character) (why not just use `r`?)
* `S`  stands for  cc  (change a whole line)

#### Where to put the count

The commands `3dw` and `d3w` both delete three words, but `3dw` deletes one word three times and `d3w` deletes three words once. Functionally there's no difference and `p` will paste the same contents. Counts can also be chained, so `2d3w` would delete 6 words, but this doesn't seem too useful.

### 04.3 Repeating a Change

The `.` command is a simple yet powerful command, it repeats the last change. Specifically it repeats the last command, do `df>` can be used to delete HTML tags regardless of which tag it is or whether it's a start or an end tag as the command will simply delete upto and including the `>`. The `.` command works for all changes made except for those made with `u`, `C-r`, and colon commands (`:`). This could be used as an alternative to interactive find and replace, instead search for a word, then use the change command, then go to the next instance with `n` and use `.` to change it.

### 04.4 Visual Mode

Visual mode is accessed with `v` or `V` and then normal navigation can be used to select text. When text is selected it can be written out to a file with `:w` or deleted with `d`, etc. Visual mode can easily be combined with other commands. To escape Visual mode just use `<Esc>`.

* `v` - enter visual mode
* `V` - enter visual mode and select whole lines
* `C-v` - enter visual mode and select via a block
* `o` - while in visual mode switch the end of the selection, use `O` to switch diagonals when in block selection mode

### 04.5 Moving Text

* `p` pastes text after the cursor or on the line below
* `P` pastes text before the cursor or on the line above
* Counts can be used with `p` and `P`
* `xp` swapping two characters, useful when correcting common typos such a 'teh' to 'the'

### 04.6 Copying Text

Yanking is used to copy text in Vim, `c` was already taken so `y` had to make do.

* `yw` - yanks a word
* `y2w` - yanks two words
* `ye` - copy a word and avoid copying the whitespace after a word
* `YY` - copies a whole line
* `y$` - yanks to the end of the line

### 04.7 Using the Clipboard

This is inconsistent between vim, neovim, and gvim (GUI Vim).

Pasting with `Cmd-V`:

In TUI Vim/Neovim `Cmd-V` will work in insert mode only (it seems).
In gvim it will work in normal and insert mode, and in visual mode it will replace any highlighted text.

An alternative way to paste is `:r !pbpaste` which will read in the contents of the clipboard to the current cursor location.

Vim native way to copy and paste with clipboard:

* `"*y` this will yank, combined with a motion, e.g. `"*ye` will yank the current word, this can be combined with visual mode, select the text to copy and then use `"*y` while in visual mode
* `"*p` this will paste/put, `"*P` will paste before the cursor. It can also be combined with a count, e.g. `"*5p` will paste the contetns five times.

### 04.8 Text Objects

When the cursor is in the middle of a word and the word is to be deleted, it may seem like the way to do it is `bdw`, but an alternative is `daw`, read as 'delete a word'. In this instance the `d` is an operator and the `aw` is a text object. Text objects are the third way to makes changes in Vim after operator-motion and Visual mode. This adds operator-text objects. The main differntiator here is the location of the cursor matters less and instead treats the text object as a whole (of course the cursor still needs to be within the text object).

* `daw` - deletes a word, regardless of where the cursor is in the word
* `2daw` - delete two words, cursor can be midway through first word, `d2aw` also works
* `cis` - 'change in sentence' deletes a sentence and switches to insert mode. This works across multiple lines even with line breaks/carriage returns.
* `dis` - deletes a sentence
* `as` - 'as sentence' or 'a sentence' text object, the difference to the `is` 'is sentence' text object is that `as` includes the white space after the sentence.

Text objects also work in Visual mode, so `vas` would select the current sentence, using `as` again would select a second sentence, using `oas` would switch direction and select a sentence at the other end.

The help pages have a list of text objects at 'text-objects'.

TKTK - lots more to text objects than what's written here.

### 04.10 Conclusion

Additional commands:

* `~` - can be used to change the case of a character, when used in visual mode any highlighted character is affected, can be configured with option 'tildeop'
* `10~` - change 10 characters case
* `vjj~` - switch to visual mode, move forward two lines, convert all highlighted characters to opposite case.

## 05 Set Your Settings

Tuning Vim, this chapter shows how to configure Vim with startup options, add packages and plugins, and define macros.

### 05.1 The vimrc file

This is the runtime configuration file for Vim, with Vim/MacVim etc it is `~/.vimrc`, but with Neovim which adheres to the XDG specification it is `~/.config/nvim/init.vim`. Although the Neovim file can be set up to source the normal .vimrc from its usual location. With Neovim check `:h init.vim` for more options.

Setting options in this file is as easy as adding a line such as `set ignorecase` so that case is always ignored in searches.

Shortcut to edit this file: `:edit $MYVIMRC`.

### 05.2 Example vimrc explained

The example vimrc that comes with neovim (don't think vim comes with one), available from `$VIMRUNTIME`, Neovim will tab complete this environment variable.

* `set showcmd` - show the current incomplete command, e.g. `2f` will show in the bottom right corner of the page until the search character is typed.
* `map Q gq` - defines a key mapping, in this case mapping `Q` to the command `gq`, this also stops the current `Q` command from working which enters Ex mode (not a very useful feature).
* `filetype plugin indent on` - this does 3 things
  * Filetype detection: VIm will recognise the type of file which can be useful for syntax hightlighting, it can tell from a file ending, e.g. `.c` or a hashbang at the start of a file `#!/bin/sh`. See 'filetypes' for more info in help.
  * Using filetype plugin files
  * Using indent files, allows Vim to compute the indent of a line automatically, see the help for options 'filetype-indent-on' and 'indentexpr'.

Example vimscript if statement that checks if colours are available before setting syntax and search hylighting:

```vim
if &t_Co > 2 || has("gui_running")
  syntax on
  set hlsearch
endif
```

There's more info in the manual section that isn't covered here.

### 05.3 Simple Mappings

A mapping makes it possible to bind a set of Vim commands to a single key. E.g. to surround certain words with curly braces using F5 use: `:map <F5> i{<Esc>ea}<Esc>`, to use this simply place the cursor on the first letter and then hit `<F5>`. The command works the same way that manually doing the process does, switches to inset mode and types the curly braces, switches to normal mode and moves to end of word, appends curly brace and switches back to normal mode. The danger here is in overriding an existing Vim command which will then no longer work.

A key that can be safely (?) used with personal mappigns is the backslash, `\`.
The `:map` command lists the current mappings, `:imap` for Interactive mode mappings.

### 05.4 Adding a Package

A package is a set of files that can be added to Vim, simples. There are two kinds: optional and automatically loaded on startup.

Vim comes with with a few packages that can be optionally used, e.g. the vimball plugin which supports creating and using vimballs (self-installing Vim plugin archives). To start using the vimball plugin add the line `packadd vimball` to .vimrc, or try it out with the colon command. For more about vimball see `:help vimball` (vimball needs to be enabled first).

What differntiates a package and a plugin?

For help on packages see `:h packages`.

### 05.5 Adding a Plugin

A plugin extends Vim's functionality and is just a Vim script file that is loaded automatically when Vim starts. A plugin can be added by dropping it in the plugin directory.

There are two types of plugins:

* global plugin: used for all kinds of file
* filetype plugin: only used for specific type of file (e.g. language specific)

#### Global Plugins

#### Filetype Plugins

### 05.6 Adding a help file

Explains how to manually add the help files of a plugin and generate the tags, which is covered by using a plugin manager. May revisit this.

### 05.7 The Option Window

To find an option there are a couple options (heh), the options help page or the `:options` command, there's also the 'option-list' linked to from the help page.

The `:options` command opens a new window with a list of options, grouped by subject, each with a one-line explainer. A subject can be jumped to via the cursor and `<Enter>`, to jump back use `<Enter>` again or `C-o`. Hitting `<Enter>` on one of these options will toggle it, which will be shown by the line switching the two options e.g. `set wrap    nowrap` will switch to `set nowrap    wrap`. Hitting enter (anywhere) on the line above with the description of the option will open the full help for it (instead of the short description).

For options that take a non-boolean (String or number) value, these can be manually edited, to apply the edit use `<Enter>`.

### 05.8 Often Used Options

Some of the more useful options that can be set (to find out more about them use single quotes with the help command e.g.: `h 'wrap'`)