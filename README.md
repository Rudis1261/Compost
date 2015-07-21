### PHP Compost Class

Open a terminal and start playing.

#### Clone in
```shell
git clone git@github.com:drpain/Compost.git
cd Compost
```

#### Like Docker, run this with it :-D
```shell
docker run -it --rm --name PHP-Compost \
-v "$PWD":/usr/src/myapp \
-w /usr/src/myapp 
php:5.6-cli php index.php
```

Hopefully you have Docker installed already, otherwise this will not work. 

```php
<?php

// This index is to show you how to make use of Compost Minifier.
// Ensure that we know where the asset paths are located relative to the assets.
define('PWD', getcwd());


// Optional Constants to help replace Site Url and Img Url this the host
define('SITE_URL', 'http://example.com'); // Optional
define('IMG', 'http://img.example.com');  // Optional

// Include the compost class
require_once('class.compost.php');

// Construct JS, the type is detected based on the name of the file provided
// This reads the information from the relative path of assets/<type>
// In this case assets/js
$JS = new Compost();
$JS->add("jquery.js");
$JS->add("custom.js");

// Similarly we can construct one for CSS
// As read from assets/css
$CSS = new Compost();
$CSS->add("bootstrap.css");
$CSS->add("custom.css");

// Now this can establish a baseline for your assets, and you can inject this into
// Your controllers and append more page specific assets to it.
// Once you are ready to get the result
// We can either print it out as is. Or return the URL of the asset

// We can print out the URL to be inserted into the document
echo $JS->url() . PHP_EOL;
echo $CSS->url() . PHP_EOL;

// Or we can get the RAW contents. Not sure when I used this. But there was a reason
echo $JS->raw() . PHP_EOL;
echo $CSS->raw() . PHP_EOL;

// CALLING ->url() renders all the files out, and uses the MD5 hash of it's contents as it's name

// Want assets specific to the header and footer?
// By default added to the 'footer' section
// Just add 'header' or 'footer' as a second parameter for add('file', 'header'), and as a optional parameter for url(header)
$JS->add("jquery.js", "header");
echo $JS->url("header") . PHP_EOL;
