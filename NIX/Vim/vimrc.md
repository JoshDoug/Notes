# Setting up a vimrc
Cover plugins here as well or separately? Break out into own file if it gets extensive

```

:imap jj <Esc>

set relativenumber
if v:version > 703
	set number
endif

set tabstop=2       " The width of a TAB is set to 2.
                    " Still it is a \t. It is just that
                    " Vim will interpret it to be having
                    " a width of 2.

set shiftwidth=2    " Indents will have a width of 2

set softtabstop=2   " Sets the number of columns for a TAB

set expandtab       " Expand TABs to spaces

```
