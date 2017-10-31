# Typical Tmux Commands

Tmux commands and shortcuts. Some of the shortcuts such as the pane resizing shortcuts are not the default bindings, these notes are specific to the linked configuration.

Leader key (LK) default binding: `C-b`

LK rebound to: ``` ` ```

Tmux configuration [here](https://github.com/JoshDoug/dotfiles/blob/master/.tmux.conf).

Tmux version: `tmux -V`, no idea why but it needs to be a capital V, who cares about consistency or convention right?

## Tmux Sessions

## Tmux Windows

* Create window: `LK c`
* Name window: `LK ,`

## Tmux panes

* Vertical split pane: `LK |` (includes Shift for the pipe symbol)
* Horizontal split pane: `LK -`
* Resize panes to the left, down, up, right: `alt h`, `alt j`, `alt k`, `alt l`, where alt and letter can both be held to instead of repeatedly being pressed.