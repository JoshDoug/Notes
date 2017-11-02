# Vim Help

Using Vim's help system, because I can never remember how.

* Navigate help like normal: h,j,k,l.
* Exit like normal: `:q` will close the help pane/window

Jump to a subject: With the cursor on a tag, highlighted in blue (?), hit `C-]` or with a mouse just double click. This will also work on non-tag words as Vim will try and find help for it, this may work better for options in single quotes.
Jump back with `C-t` or `C-o`, repeat to go further back.

Get specific help on a command with `:help command`, context can be prepended:

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
