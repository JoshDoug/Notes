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
* `set relativenumber` - set relative line numbers, when combined with `set number` the current line has an absolute number while the rest are relative
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