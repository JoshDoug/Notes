# Typical Tmux Commands

Tmux commands and shortcuts. Some of the shortcuts such as the pane resizing shortcuts are not the default bindings, these notes are specific to the linked configuration.

Basics:

* Leader key (LK) default binding: `C-b`
* LK rebound to: ``` ` ```
* Tmux configuration [here](https://github.com/JoshDoug/dotfiles/blob/master/.tmux.conf).
* Tmux version: `tmux -V`, no idea why but it needs to be a capital V, who cares about consistency or convention right?
* List shortcuts: `LK ?`

## Tmux Sessions

To start a new session, just run `tmux`. The session number is shown at the bottom left of the window, like so: `[0]`.

## Tmux Windows

* Create window: `LK c`
* Name the current window: `LK ,`
* Switch to next or previous window: `LK n` for next window, `LK p` for previous window, or rebound to `Shift Left` to move left or `Shift Right` to move right, which can be used to loop through all the windows of a session.
* Switch to the last used window: `LK l`
* Close window: `LK &`, this will ask for confirmation and then close any panes within the window.
* List windows: `LK w`, this will list the windows which can be navigated by arrow keys and selected with enter.

## Tmux panes

* Vertical split pane: `LK |` (includes Shift for the pipe symbol)
* Horizontal split pane: `LK -`
* Resize panes to the left, down, up, right: `alt h`, `alt j`, `alt k`, `alt l`, where alt and letter can both be held to instead of repeatedly being pressed.