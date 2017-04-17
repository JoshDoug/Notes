# Installing an AMP Environment
## Manually
Useful tutorials:
* [Apache, MySql, PHP, Homebrew, Sierra](https://lukearmstrong.github.io/2016/12/setup-apache-mysql-php-homebrew-macos-sierra/)
* [Apache, MySQL, PHP, PhpMyAdmin, El Capitan](https://maltronic.io/2016/10/23/easily-install-php-with-apache-mysql-and-phpmyadmin-on-mac-os-x-el-capitan/)

### Installing php
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

## MAMP
Just download and install, make sure errors are on etc.

## Docker, Vagrant, etc...

# Variables
PHP is a dynamic language, although strict types can be used.

`
$myVar = 1;
`

Strict types: TODO

# Arrays


# Conditionals
If

Switch

# Loops
As with conditionals, there are two syntactic options for loops, braces or colon.

```
//Braces
for($i = 0; $i <= 10; $i++) {
  echo $i;
}

//Colon
<?php for($i = 0; $i <= 10; $i++) : ?>
  <p><?= $i ?></p>
<?php endfor ?>

```

# Function

```
<?php
function getCopyRight($startYear) {
    $currentYear = date('Y');
    if($startYear < $currentYear) {
        $currentYear = date('y');
        return "&copy; $startYear&ndash;$currentYear";
    } else {
        return "&copy; $startYear";
    }
}

echo getCopyRight(2015);
?>
```

# Paths & Includes
Server side includes allow pages to include commonly repeated content (HTML)
that is kept in an external file. This is popularly used with navs, headers, and footers.
This avoids redundant code and creates a single point to edit, instead of having to edit several
pages to reflect a single navigation change (for example).

<?php

//Not really necessary if using a virtual host
$siteRoot = '/path/to/root';

//Required - page will not load without it
require './includes/header.php';
//Include - just gets skipped if the file isn't located
include './includes/footer.php';

?>

## Using Paths Within Include content

```
//Set at the start of the php file which will use the includes, .e.g index.php
//Again - less important if using a virtual host
$siteRoot = '/path/to/root';

//The site root variable can then be used by the files that are being included, e.g. header.php
<img src="<?= $siteRoot; ?>/images/artists/artist.png" alt="artist">

```
