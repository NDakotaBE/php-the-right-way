---
title:   Werken met UTF-8
isChild: true
anchor:  php_and_utf8
---

## Werken met UTF-8 {#php_and_utf8_title}

_Deze sectie is oorspronkelijk geschreven door [Alex Cabal](https://alexcabal.com/) van 
[PHP Best Practices](https://phpbestpractices.org/#utf-8) en is gebruikt als basis van dit UTF-8 advies_.

### Er is geen one-liner. Wees voorzichtig, gedetaileerd en consequent.

Op dit moment ondersteund PHP geen Unicode op het basis niveau. 
Er zijn manieren beschikbaar die er voor zorgen dat UTF-8 strings correct verwerkt worden.
Deze zijn echter niet evident en vereisen een aantal aanpassingen doorheen alle niveaus van een web-app, van HTML tot SQL tot PHP.
We proberen hieronder een korte en praktische samenvatting te maken.

### UTF-8 op PHP niveau

De basis string operaties, zoals het samenvoegen van twee strings en het assignen van strings aan variabelen hebben geen speciale behandeling nodig voor UTF-8.
Het is echter wel zo dat de meeste string functies, zoals `strpos()` en `strlen()`, extra overweging vereisen.
Deze functies hebben meestal een `mb_*` variant. Bijvoorbeeld `mb_strpos()` en `mb_strlen()`.
Die functies worden beschikbaar gemaakt door de [Multibyte String Extensie] en is specifiek gemaakt om Unicode strings te verwerken.

Je moet gebruik maken van de `mb_*` functies wanneer je werkt met een Unicode string. Wanneer je bijvoorbeeld `substr()` gebruikt op een UTF-8 string bestaat de kans dat het resultaat een aantal vreemde karakters zal bevatten.
De correcte functie om hier te gebruiken is dan de `mb_substr()` functie.

Het moeilijkste deel is dan ook om de `mb_*` functies altijd te gebruiken. Wanneer je dit ook maar één keer vergeet, bestaat de kans de een Unicode string onleesbaar wordt voor verdere verwerking.

Niet alle string functies hebben een `mb_*` tegenhanger. Als dit het geval is dan heb je pech.

Je dient ook gebruik te maken van de `mb_internal_encoding()` functie aan het begin van elk van je PHP scripts te plaatsen (of aan het begin van je globaal include script).
Ook de `mb_http_output()` functie is vereist net voor je output naar de browser stuurt.
Het expliciet definiëren van de encoding van je strings in elk script zal veel problemen verhelpen.

Sommige PHP functies, die met strings werken, hebben een optionele parameter die je toelaat om de karakter encoding mee te geven.
Je dient altijd aan te duiden dat je met UTF-8 werkt, wanneer de optie beschikbaar is.
De functie `htmlentities()` heeft bijvoorbeeld een optie om karakter encoding mee te geven.

**Let op:** Sinds PHP 5.4.0 is UTF-8 de standaard encoding voor `htmlentities()` en `htmlspecialchars()`.

Wanneer je een applicatie bouwt, die gedistribueerd wordt en je niet zeker kan zijn dat de `mbstring` extensie geladen is, is het interessant om de [patchwork/utf8] Composer package te gebruiken.
Deze package maakt gebruik van de `mbstring` extensie wanneer deze beschikbaar is en zal anders terugvallen op niet UTF-8 compatibele functies.

[Multibyte String Extensie]: https://secure.php.net/book.mbstring
[patchwork/utf8]: https://packagist.org/packages/patchwork/utf8

### UTF-8 op database niveau

Wanneer je PHP script toegang nodig heeft tot MySQL dan bestaat de kans dat je strings opgeslagen wordenals niet UTF-8 strings in de database. Zelfs wanneer je alle raad van hierboven volgt.

Om zeker te zijn dat de strings in UTF-8 van PHP naar MySQL gaan, dien je je database en tabellen in te stellen met de `utf8mb4` collation en karakters.
Het is ook belangerijk om in je PDO connection string `utf8mb4` toe te voegen als character set.
Dit is _enorm belangerijk_.

Zorg er ook voor dat je `utf8mb4` gebruikt voor een complete UTF-8 ondersteuning en niet `utf8`!
Bekijk het hoofdstuk "Meer lezen" voor meer informatie

### UTF-8 at the browser level

Use the `mb_http_output()` function to ensure that your PHP script outputs UTF-8 strings to your browser.

The browser will then need to be told by the HTTP response that this page should be considered as UTF-8. Today, it is common to set the character set in the HTTP response header like this:

{% highlight php %}
<?php
header('Content-Type: text/html; charset=UTF-8')
{% endhighlight %}

The historic approach to doing that was to include the [charset `<meta>` tag](http://htmlpurifier.org/docs/enduser-utf8.html) in your page's `<head>` tag.

{% highlight php %}
<?php
// Tell PHP that we're using UTF-8 strings until the end of the script
mb_internal_encoding('UTF-8');
$utf_set = ini_set('default_charset', 'utf-8');
if (!$utf_set) {
    throw new Exception('could not set default_charset to utf-8, please ensure it\'s set on your system!');
}

// Tell PHP that we'll be outputting UTF-8 to the browser
mb_http_output('UTF-8');
 
// Our UTF-8 test string
$string = 'Êl síla erin lû e-govaned vîn.';

// Transform the string in some way with a multibyte function
// Note how we cut the string at a non-Ascii character for demonstration purposes
$string = mb_substr($string, 0, 15);

// Connect to a database to store the transformed string
// See the PDO example in this document for more information
// Note the `charset=utf8mb4` in the Data Source Name (DSN)
$link = new PDO(
    'mysql:host=your-hostname;dbname=your-db;charset=utf8mb4',
    'your-username',
    'your-password',
    array(
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_PERSISTENT => false
    )
);

// Store our transformed string as UTF-8 in our database
// Your DB and tables are in the utf8mb4 character set and collation, right?
$handle = $link->prepare('insert into ElvishSentences (Id, Body, Priority) values (default, :body, :priority)');
$handle->bindParam(':body', $string, PDO::PARAM_STR);
$priority = 45;
$handle->bindParam(':priority', $priority, PDO::PARAM_INT); // explicitly tell pdo to expect an int
$handle->execute();

// Retrieve the string we just stored to prove it was stored correctly
$handle = $link->prepare('select * from ElvishSentences where Id = :id');
$id = 7;
$handle->bindParam(':id', $id, PDO::PARAM_INT);
$handle->execute();

// Store the result into an object that we'll output later in our HTML
// This object won't kill your memory because it fetches the data Just-In-Time to
$result = $handle->fetchAll(\PDO::FETCH_OBJ);

// An example wrapper to allow you to escape data to html
function escape_to_html($dirty){
    echo htmlspecialchars($dirty, ENT_QUOTES, 'UTF-8');
}

header('Content-Type: text/html; charset=UTF-8'); // Unnecessary if your default_charset is set to utf-8 already
?><!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>UTF-8 test page</title>
    </head>
    <body>
        <?php
        foreach($result as $row){
            escape_to_html($row->Body);  // This should correctly output our transformed UTF-8 string to the browser
        }
        ?>
    </body>
</html>
{% endhighlight %}

### Further reading

* [PHP Manual: String Operations](https://secure.php.net/language.operators.string)
* [PHP Manual: String Functions](https://secure.php.net/ref.strings)
    * [`strpos()`](https://secure.php.net/function.strpos)
    * [`strlen()`](https://secure.php.net/function.strlen)
    * [`substr()`](https://secure.php.net/function.substr)
* [PHP Manual: Multibyte String Functions](https://secure.php.net/ref.mbstring)
    * [`mb_strpos()`](https://secure.php.net/function.mb-strpos)
    * [`mb_strlen()`](https://secure.php.net/function.mb-strlen)
    * [`mb_substr()`](https://secure.php.net/function.mb-substr)
    * [`mb_internal_encoding()`](https://secure.php.net/function.mb-internal-encoding)
    * [`mb_http_output()`](https://secure.php.net/function.mb-http-output)
    * [`htmlentities()`](https://secure.php.net/function.htmlentities)
    * [`htmlspecialchars()`](https://secure.php.net/function.htmlspecialchars)
* [Stack Overflow: What factors make PHP Unicode-incompatible?](https://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)
* [Stack Overflow: Best practices in PHP and MySQL with international strings](https://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)
* [How to support full Unicode in MySQL databases](https://mathiasbynens.be/notes/mysql-utf8mb4)
* [Bringing Unicode to PHP with Portable UTF-8](https://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)
* [Stack Overflow: DOMDocument loadHTML does not encode UTF-8 correctly](https://stackoverflow.com/questions/8218230/php-domdocument-loadhtml-not-encoding-utf-8-correctly)
