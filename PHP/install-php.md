# Setting up PHP

## macOS

From source: don't.

Using a package manager: brew, which installs source but automates process.
PHP specific info when using brew here: https://github.com/Homebrew/homebrew-php

Using pre-installed system php: avoid if possible (outdated).

Installing a binary: Use MAMP.

## Windows

## Linux

## __Installing an AMP Environment__

## Manually

Useful tutorials:

* [Apache, MySql, PHP, Homebrew, Sierra](https://lukearmstrong.github.io/2016/12/setup-apache-mysql-php-homebrew-macos-sierra/)
* [Apache, MySQL, PHP, PhpMyAdmin, El Capitan](https://maltronic.io/2016/10/23/easily-install-php-with-apache-mysql-and-phpmyadmin-on-mac-os-x-el-capitan/)

### Installing PHP

php71-fpm installed with homebrew, php71-fpm restart|start|stop, and using default port 9000.

### Installing Apache

### Installing MySQL

### Installing PHPMyAdmin

brew install phpmyadmin

Neat tool for creating a blowfish hash: http://www.passwordtool.hu/blowfish-password-hash-generator
Hopefully safe...only using in a testing environment though.

#### [Configuring pma user](http://foundationphp.com/tutorials/pma_config.php)

Make sure when creating the pma user to add a special character, e.g. *, ! won't cut it. To check password requirements, [link](https://gsuartana.wordpress.com/2016/08/18/mysql-error-1819-hy000-your-password-does-not-satisfy-the-current-policy-requirements/).
mysql.host table is deprecated and removed, so remove that row when running the SQL queries.

### Commands when working with AMP

If you're not using ports that require root privs then you don't need to start apachectl as root.
PHP warns against being started as a normal user, `'user' directive is ignored when FPM is not running as root` but it doesn't seem to make any practical difference. To run either as root just preface the relevant command with `sudo`.

Apache: `apachectl start|restart|graceful|graceful-stop|stop` etc
PHP: `php71-fpm start|stop|force-quit|restart|reload|status|configtest` etc
MySQL: `mysql.server start|stop|restart|reload|force-reload|status` etc

Most of a help option to find other commands.

## MAMP

Just download and install, make sure errors are on etc.

## Docker, Vagrant, etc...