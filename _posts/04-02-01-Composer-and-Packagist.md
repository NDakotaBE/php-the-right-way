---
title:   Composer en Packagist
isChild: true
anchor:  composer_and_packagist
---

## Composer en Packagist {#composer_and_packagist_title}

Composer is de aangeraden dependency manager voor PHP. Lijst je projects dependencies op in een `composer.json` bestand.
Hierna kan Composer, na het invoeren van een aantal simpele commando's, automatisch je projects dependencies ophalen en autoloading instellen voor je.
Composer valt te vergelijken met NPM in node.js of Bundler bij Ruby.

Er is een verscheidenheid aan PHP libraries die compatibel zijn met Composer en dus klaar zijn om te gebruiken in je project.
Deze "packages" worden opgelijst op [Packagist], de officiële repository voor Composer-compatibele PHP libraries.

### Hoe Composer installeren

De veiligste manier om composer te downloaden is door de [officiële instructies te volgen](https://getcomposer.org/download/).
Deze zal verifiëren of de installer niet corrupt of aangepast is en installeert een `composer.phar` binary in je _huidige working directory_.

We bevelen echter aan om Composer *globaal* te installeren (bijvoorbeeld een kopie in `/usr/local/bin`). Om dit te doen kun je gebruik maken van het onderstaande commando:

{% highlight console %}
mv composer.phar /usr/local/bin/composer
{% endhighlight %}

**Let op:** Als het bovenstaande commando faalt, door rechten, plaats je hier `sudo` voor.

Om vanuit je _working directory_ composer te gebruiken kun je `php composer.phar` uitvoeren.
Wanneer deze globaal geïnstalleerd is, kun je dit simpelweg doen door `composer` te gebruiken.

#### Installatie (Windows)


Als Windows gebruiker is de installatie van composer het eenvoudigst door de [ComposerSetup] te gebruiken.
Deze voert een globale installatie uit en stelt het `$PATH` in, waardoor je `composer` kan gebruiken vanuit elke directory op de commandline.

### Hoe dependencies installeren en beheren

Composer houdt de dependencies van je project bij in een bestand `composer.json`. 
Je kan de inhoud van dit bestand manueel beheren of door gebruik te maken van Composer zelf.
Het `composer require` commando voegt een dependency aan je project toe en wanneer er geen `composer.json` bestaat zal deze aangemaakt worden.
Hieronder vind je een voorbeeld om [Twig] toe te voegen als dependency aan je project.

{% highlight console %}
composer require twig/twig:^2.0
{% endhighlight %}

Een andere optie is het commando `composer init`.
Dit commando gidst je door het aanmaken van een volledig `composer.json` bestand voor je project.

Welke manier je ook verkiest, eenmaal een `composer.json` bestand beschikbaar is, kun je Composer de opdracht geven om alle project-dependencies te downloaden en te installeren.
De installatie van deze bestanden wordt uitgevoerd in de `vendor/` map van je project.

Dit is ook van toepassing voor alle projecten waar een `composer.json` bestand in beschikbaar is.

{% highlight console %}
composer install
{% endhighlight %}

Vervolgens voegen we de instructie toe om Composer te gebruiken doorheen je volledige project.
Dit wordt gedaan in een file die door je volledige applicatie gebruikt wordt.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Nu kun je gebruik maken van je project dependencies en zullen ze ge-autoload zijn op aanvraag.

### Updaten van je dependencies

Composer maakt een bestand aan met de naam `composer.lock` die bijhoudt welke exacte versie van je packages gedownload zijn, wanneer je `composer install` uitgevoerd hebt.
Wanneer je dit project wilt delen met anderen dien je er voor te zorgen dat je `composer.lock` bestand beschikbaar is. Hierdoor kunnen zij `composer install` uitvoeren en worden dezelfde versies van packages geïnstalleerd als bij jou.

Om je dependencies up te daten, voer je `composer update` uit. 
Gebruik dit commando niet om te deployen, maar gebruik `composer install` aangezien je met andere versies van packages kan eindigen op de productie omgeving.

Composer laat je ook toe om flexibel om te gaan met de versies van packages die je download.
Je kan bijvoorbeeld een noodzaak hebben voor `~1.8` waardoor alle versies groter dan `1.8.0` en kleiner dan `2.0.x-dev` zullen geïnstalleerd worden.
Je kan ook gebruik maken van `*`, wat zal zorgen dat alle `1.8.*` versies geïnstalleerd kunnen worden.
Hierna zal het `composer update` commando al je dependencies updaten naar de laatste versie, rekening houdend met de restricties die ingesteld zijn.

### Update notificaties

Om notificaties over updates te ontvangen kun je je inschrijven op [libraries.io].
Dit is een web service die je dependencies kan monitoren en die je een melding zal geven wanneer een update beschikbaar is.

### Controle van dependencies op security issues

De [Security Advisories Checker] is een web service en commandline tool die je `composer.lock` file bestudeert. Hierna krijg je een melding of je je dependencies **moet** updaten.

### Globale dependencies met Composer

Composer kan ook gebruikt worden om globale dependencies en hun binaries te managen.
Het gebruik hiervan is relatief simpel. Het enige wat je hiervoor moet doen is je commando prefixen met `global`.
Wanneer je bijvoorbeeld PHPUnit wilt installeren en je dient deze globaal beschikbaar te hebben, kun je onderstaand commando gebruiken:

{% highlight console %}
composer global require phpunit/phpunit
{% endhighlight %}

Dit maakt een `~/.composer` map aan, waar al je globale dependencies in opgeslagen worden.
Om deze packages overal beschikbaar te hebben, dien je de `~/.composer/vendor/bin` map toe te voegen aan je 
`$PATH` variabele.

* [Lees meer over Composer]

[Packagist]: https://packagist.org/
[Twig]: https://twig.symfony.com/
[libraries.io]: https://libraries.io/
[Security Advisories Checker]: https://security.sensiolabs.org/
[Lees meer over Composer]: https://getcomposer.org/doc/00-intro.md
[ComposerSetup]: https://getcomposer.org/Composer-Setup.exe
