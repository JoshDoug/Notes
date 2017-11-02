# PhpStorm

An IDE built upon the IntelliJ IDEA platform, that supports PHP & SQL DBs.
PhpStorm = WebStorm + PHP + DB/SQL, so all the features of WebStorm are included into PhpStorm, and full-fledged support for PHP and Databases/SQL support are added on top.

Links:

* [Quick Start Guide](https://www.jetbrains.com/help/phpstorm/2017.1/quick-start-guide.html)
* [Tutorials](https://confluence.jetbrains.com/display/PhpStorm/Tutorials)
* [PhpStorm Blog](https://blog.jetbrains.com/phpstorm/)
* [PhpStorm Page](https://www.jetbrains.com/phpstorm/)
* [PhpStorm for Users of Text Editors](https://confluence.jetbrains.com/display/PhpStorm/PhpStorm+for+Users+of+Text+Editors)
* [PhpStorm Video Tutorials](https://www.jetbrains.com/phpstorm/documentation/phpstorm-video-tutorials.html)

## Quick Start Guide Notes

### Step 0: Before you start

PhpStorm support PHP version 5.3+, as well as HTML, CSS, JavaScript, and XML which are pugins bundled with the IDE and activated by default. Plugins can be used to add support for other langauges and features. It runs on Windows, macOS, and Linux. Runs with a bundled version of the JRE.

#### Configuring PHP Environment

Configuring PhpStorm relies on setting it up in an environment with [XAMPP](https://confluence.jetbrains.com/display/PhpStorm/Installing+and+Configuring+XAMPP+with+PhpStorm+IDE), [MAMP](https://confluence.jetbrains.com/display/PhpStorm/Installing+and+Configuring+MAMP+with+PhpStorm+IDE), or [Docker](https://confluence.jetbrains.com/display/PhpStorm/Docker+Support+in+PhpStorm). Also see [Vagrant Support](https://confluence.jetbrains.com/display/PhpStorm/Getting+started+with+Vagrant+in+PhpStorm) and [Vagrant Tool](https://www.jetbrains.com/help/phpstorm/2017.1/vagrant.html).

##### Using Vagrant

* [Vagrant](https://www.vagrantup.com/)
* [PhpStorm Vagrant Help](https://www.jetbrains.com/help/phpstorm/2017.1/vagrant.html)
* [PhpStorm Confluence Vagrant Support](https://confluence.jetbrains.com/display/PhpStorm/Getting+started+with+Vagrant+in+PhpStorm)
* [PuPHPet](https://puphpet.com/) - a GUI configurator for Vagrant using [Puppet](https://puppet.com/) for provisioning.
* [PhpStorm Vagrant Video Tutorial](https://www.youtube.com/watch?v=f7Kss62DHhw)

##### Using Docker

TODO

##### [Using MAMP](https://confluence.jetbrains.com/display/PhpStorm/Installing+and+Configuring+MAMP+with+PhpStorm+IDE)

Adding PHP - just set the path to the PHP install, provided by MAMP/System/Manual/Brew install.
Adding the Debugger - [Xdebug](https://confluence.jetbrains.com/display/PhpStorm/Xdebug+Installation+Guide) or [Zend Debugger](https://confluence.jetbrains.com/display/PhpStorm/Zend+Debugger+Installation+Guide)

##### DIY with HomeBrew

Useful guide: [Setup Apache Mysql and PHP with Homebrew on macOS Sierra](https://lukearmstrong.github.io/2016/12/setup-apache-mysql-php-homebrew-macos-sierra/)
See also: PHP/language-basics.md

* [Configure PHP, Apache, and MySQL](https://confluence.jetbrains.com/display/PhpStorm/Installing+and+Configuring+MAMP+with+PhpStorm+IDE), ignore the MAMP stuff, doesn't really matter.
* [Xdebug](https://confluence.jetbrains.com/display/PhpStorm/Xdebug+Installation+Guide), should have been installed with homebrew already at this point.

With everything setup and working (PHP, Xdebug, Apache, MySQL, PHPMyAdmin, with no errors showing and a phpinfo page loaded), add everything into PhpStorm.

In settings, add PHP which should automatically find Xdebug, Apache just specifies the location under Deployment > Servers, MySQL is set up in the Databases part, select + and choose MySQL (or whichever relevant DB driver).
