---
anchor: code_style_guide
---

# Code Style Guide {#code_style_guide_title}

De PHP community is groot en divers en bestaat uit ontelbare libraries, frameworks en componenten.
Het is gebruikelijk voor PHP ontwikkelaars om verschillende van deze te kiezen en deze te combineren in een enkel project.
Het is dus belangerijk dat PHP code een gedeelde code style (zo goed als mogelijk) volgen zodat
ontwikkelaars gemakkelijk verschillende libraries kunnen combineren in hun projecten.

De [Framework Interop Group][fig] heeft een aantal stijl aanbevelingen voorgesteld en goedgekeurd.
Niet al deze voorstellen zijn gerelateerd aan code-style, maar diegene die dit wel zijn, zijn de volgende: [PSR-1][psr1], [PSR-2][psr2] en [PSR-4][psr4].
Deze aanbevelingen zijn enkel een set met regels die vele projecten zoals Drupal, Zend, Symfony, Laravel, CakePHP, phpBB, AWS SDK,
FuelPHP, Lithium en dergelijke overnemen.
Je kunt deze gebruiken voor je eigen projecten of je eigen persoonlijke stijl gebruiken.

Je kan best PHP code schrijven die een bestaande standaard implementeert.
Dit kan iedere combinatie van PSR's zijn of een coding standard uitgegeven door PEAR of Zend.
Dit zorgt er dan voor dat andere ontwikkelaars je code gemakkelijk kunnen lezen en bewerken.
Dit zorgt er ook voor dat applicaties die veel externe code implementeren consequent kunnen zijn en blijven.

* [Lees over PSR-1][psr1]
* [Lees over PSR-2][psr2]
* [Lees over PSR-4][psr4]
* [Lees over PEAR Coding Standards][pear-cs]
* [Lees over Symfony Coding Standards][symfony-cs]

Je kunt [PHP_CodeSniffer][phpcs] gebruiken om je code te controleren tegenover deze aanbevelingen en plugins voor teksteditors zoals [Sublime Text][st-cs] om real-time feedback te verkrijgen.

Je kan de lay-out van code ook aanpassen door gebruik te maken van onderstaande tools:

- [PHP Coding Standards Fixer][phpcsfixer] heeft een goed geteste codebase.
- [PHP Code Beautifier and Fixer][phpcbf] is een tool die ingebrepen is met PHP_CodeSniffer en kan gebruikt worden om je code aan te passen volgens deze aanbevelingen.

Je kan phpcs manueel vanaf commandline/shell uitvoeren door het onderstaande commando uit te voeren:

    phpcs -sw --standard=PSR2 bestand.php

De output van dit commando zal je fouten tonen en uitleggen hoe je deze oplost.
Het kan ook interessant zijn om dit commando toe te voegen aan een [git hook].
Hierdoor kun je branches beschermen tegen aanpassingen die ingaan tegen de gekozen standaard.

Wanneer je PHP_CodeSniffer gebruikt, kun je ook automatisch code lay-out problemen oplossen door gebruik te maken van 
[PHP Code Beautifier and Fixer][phpcbf].

    phpcbf -w --standard=PSR2 bestand.php

Een andere optie is gebruik te maken van [PHP Coding Standards Fixer][phpcsfixer]
Dit zal je tonen welke errors de code had alvorens deze (automatisch) opgelost waren.

    php-cs-fixer fix -v --level=psr2 bestand.php

Engels heeft de voorkeur voor de namen van variabelen en code infrastructuur. Commentaar mag geschreven worden in de taal die het gemakkelijkst leestbaar is door alle huidige (en toekomstige) partijen die met deze codebase zullen werken.

Tot slot is [Clean Code PHP][cleancode] een goede bijkomende bron om duidelijke PHP code te schrijven.

[fig]: https://www.php-fig.org/
[psr1]: https://www.php-fig.org/psr/psr-1/
[psr2]: https://www.php-fig.org/psr/psr-2/
[psr4]: https://www.php-fig.org/psr/psr-4/
[pear-cs]: https://pear.php.net/manual/en/standards.php
[symfony-cs]: https://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: https://pear.php.net/package/PHP_CodeSniffer/
[phpcbf]: https://github.com/squizlabs/PHP_CodeSniffer/wiki/Fixing-Errors-Automatically
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: https://cs.sensiolabs.org/
[cleancode]: https://github.com/jupeter/clean-code-php
[git hook]: https://git-scm.com/book/uz/v2/Customizing-Git-Git-Hooks
