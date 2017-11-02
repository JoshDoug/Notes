# Vim Help

Using Vim's help system, because I can never remember how.

To get help in Vim use `:help`, this will open the main help menu which explains how to use it.

To get help with something more specific add the search term after the help command: `:help w` to get help on writing to a file. Other examples:

* `:help c_CTRL-D` or `:help ^D`
* `:help insert-index`
* `:help user-manual`

Use `C-w C-w to jump from one window to another` and `:q` to quit help.

* Navigate help like normal: h,j,k,l.
* Exit like normal: `:q` will close the help pane/window

## Using Help Pages

List a help pages table of contents with `M-]`, this opens up in another pane which can be navigated with `j`, and `k` or arrow keys, and sections can be selected with enter which will switch to the help pane at the specified section.

Jump to a subject: With the cursor on a tag, highlighted in blue (?), hit `C-]` or with a mouse just double click. This will also work on non-tag words as Vim will try and find help for it, this may work better for options in single quotes.
Jump back with `C-t` or `C-o`, repeat to go further back.

## Help Command

Get specific help on a command with `:help command` or `:h command` for short, context can be prepended like so:

|WHAT|PREPEND|EXAMPLE|
|----|-------|-------|
|Normal mode command|                  |`:help x`|
|Visual mode command|         v_       |`:help v_u`|
|Insert mode command|         i_       |`:help i_<Esc>`|
|Command-line command|        :        |`:help :quit`|
|Command-line editing|        c_       |`:help c_<Del>`|
|Vim command argument|        -        |`:help -r`|
|Option              |       '         |`:help 'textwidth'`|
|Regular expression  |       /         |`:help /[`|

The help command can also accept wildcards such as `*` and `?`, Vim will use the best match for this instead of displaying a possible list of matches(TKTK?).

Useful help pages are listed on the main help page, but also here:

* `:h options` - options that can be set via vimrc, also `:h option-list`

## Useful Help Pages

* `:h help-summary` - summary of useful help searches
* `:h index` - get a complete index of all Vim commands