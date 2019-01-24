---
title: Installatie (Windows)
isChild: true
anchor:  windows_setup
---

## Installatie (Windows) {#windows_setup_title}

Je kan de binaries downloaden van [windows.php.net/download][php-downloads]. Na het extracten van PHP is het aangeraden om het [PATH][windows-path] in te stellen op de hoofdmap van je PHP folder (waar je php.exe staat), opdat je het kan uitvoeren van gelijk waar.

Om te leren en lokaal te ontwikkelen kan je de ingebouwde web server van PHP 5.4+ gebruiken. 
Hierdoor dien je geen rekening te houden met configuratie. 
Als je liever een "all-in-one" optie hebt, die een volledige web server en MySQL server bevat, dan zijn tools zoals [Web Platform Installer][wpi], [XAMPP][xampp], [EasyPHP][easyphp], [OpenServer][openserver] en [WAMP][wamp] aan te raden.
Deze tools laten je toe snel te starten met ontwikkelen op Windows.
Dit gezegd zijnde zullen deze tools iets anders zijn op een productie omgeving wanneer je ontwikkelingsomgeving Windows is en je productie omgeving Linux.

Wanneer je een productie omgeving op wilt zetten op Windows, dan zal IIS7 je de meeste stabiele en meest performate omgeving opleveren. Je kunt [phpmanager][phpmanager] (een gebruikersinterface voor IIS7) gebruiken om de configuratie en het beheer van PHP
simpel te maken.
IIS7 komt met FastCGI ingebouwd, waardoor je enkel PHP dient te configureren als handler. Voor meer informatie is er een [aparte omgeving op iis.net][php-iis] voor PHP.

Wanneer je applicatie in verschillende omgevingen staan voor productie en ontwikkeling kunnen vreemde bugs opduiken wanneer je live gaat. Wanneer dit het geval is, kun je een [Virtuele Machine](/#virtualization_title) overwegen.

Chris Tankersley heeft een interessante blog post over welke tools hij gebruikt om [PHP te ontwikkelen op Windows][windows-tools].

[easyphp]: http://www.easyphp.org/
[phpmanager]: http://phpmanager.codeplex.com/
[openserver]: http://open-server.ru/
[wamp]: http://www.wampserver.com/en/
[php-downloads]: http://windows.php.net/download/
[php-iis]: http://php.iis.net/
[windows-path]: http://www.windows-commandline.com/set-path-command-line/
[windows-tools]: http://ctankersley.com/2016/11/13/developing-on-windows-2016/
[wpi]: https://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
