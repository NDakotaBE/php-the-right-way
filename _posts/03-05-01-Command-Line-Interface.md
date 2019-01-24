---
isChild: true
anchor:  command_line_interface
---

## Command Line Interface {#command_line_interface_title}

PHP is gecreëerd om web applicaties mee te ontwikkelen, maar is ook interessant om command line interface (CLI) applicaties.
Command line PHP programma's kunnen helpen om veel voorkomende taken, zoals testing, deployment en applicatie administratie, te automatiseren.

CLI PHP programma's zijn krachtomg omdat deze de code van je app direct kunnen gebruiken, zonder dat er een "veilige" web GUI voor gemaakt moet worden.
Wees er zeker van om CLI PHP scripts **niet** in de publieke directory van je project te plaatsen.

Probeer PHP uit te voeren van de commandline:

{% highlight console %}
> php -i
{% endhighlight %}

De `-i` optie zal je PHP configuratie weergeven zoals de [`phpinfo()`][phpinfo] functie.

De `-a` optie zorgt voor een interactieve shell die te vergelijken valt met ruby's IRB of python's interactieve shell. 
Er zijn nog een aantal andere interessante [command line options][cli-options].

We zullen beginnen met een simpel "Hallo, $name" CLI programma te schrijven.
Om dit te testen maken we een bestand aan: `hallo.php` zoals hieronder.

{% highlight php %}
<?php
if ($argc !== 2) {
    echo "Gebruik: php hallo.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hallo, $name\n";
{% endhighlight %}

PHP stelt twee speciale variabelen in, gebaseerd op de argumenten waarmee het script uitgevoerd wordt.
[`$argc`][argc] is een integer variable dat het *aantal* argumenten bevat en [`$argv`][argv] 
is een array variable waar alle argument *waarden* in beschikbaar zijn.
Het eerste argument is steeds de naam van je PHP script bestand, in dit geval `hallo.php`

De `exit()` functie is gebruikt met een niet-nul nummer om de shell te laten weten dat het commando gefaald heeft.
Gebruikelijke exit codes kan je [hier][exit-codes] vinden.

To run our script, above, from the command line:

{% highlight console %}
> php hello.php
Usage: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}


 * [Learn about running PHP from the command line][php-cli]

[phpinfo]: https://secure.php.net/function.phpinfo
[cli-options]: https://secure.php.net/features.commandline.options
[argc]: https://secure.php.net/reserved.variables.argc
[argv]: https://secure.php.net/reserved.variables.argv
[exit-codes]: https://www.gsp.com/cgi-bin/man.cgi?section=3&amp;topic=sysexits
[php-cli]: https://secure.php.net/features.commandline.options
