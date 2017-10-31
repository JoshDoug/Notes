# Tmux Configuration File

Configuring tmux with the .tmux.conf runtime configuration file.

Handy guides and links:

* [Making tmux Pretty and Usable - Ham Vocke](http://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/)

## Setting the Leader Key bindings

```conf
# Set Leader Key but allow backticks to be typed by double tapping
unbind C-b
set-option -g prefix `
bind ` send-prefix
```

Or the more traditional:

```conf
# Set Leader Key
unbind C-b
set -g prefix `
```

## Other settings

Note: `set` is (allegedly) an alias of `set-option`, so they can both be used interchangably, so might as well just use `set` as it's shorter.

* Stop tmux from renaming window names that have been manually set: `set-option -g allow-rename off`
* Change colour of the status bar: `set -g status-bg cyan`