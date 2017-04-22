# brew.sh

The missing package manger for macOS!

Useful links:

* [github page for homebrew services](https://github.com/Homebrew/homebrew-services)

## Using brew to manage services

Start a service at login, and run it: `brew services start mysql`
Run a service (but don't start at login): `brew services run mysql`
Stop service: `brew services stop mysql`
Restart a service: `brew services restart mysql`
List services managed by brew: `brew services list`
Apply above to all services: `brew services run|start|stop|restart --all`