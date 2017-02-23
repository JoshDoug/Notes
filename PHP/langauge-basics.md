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
