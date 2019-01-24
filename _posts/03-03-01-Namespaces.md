---
isChild: true
anchor:  namespaces
---

## Namespaces {#namespaces_title}

Zoals hierboven vermeld, heeft de PHP community veel ontwikkelaars die veel code maken. 
Dit zorgt ervoor dat een library's PHP code eenzelfde klasse kan gebruiken als een ander.
Wanneer beide libraries gebruikt worden in dezelfde namespace botsen ze en zorgen ze voor problemen.

_Namespaces_ lossen dit probleem op. Zoals beschreven in de PHP referentie kunnen namespaces vergeleken worden met operating system mappen die files _namespacen_; twee bestanden met dezelfde naam bestaan naast elkaar in verschillende mappen.
Zo kun je 2 PHP classes met dezelfde naam laten bestaan in verschillende namespaces.

Het is belangerijk dat je je code _namespaced_ opdat andere ontwikkelaars deze kunnen gebruiken zonder dat deze botst met andere libraries.

Een aanbevolen manier om namespaces te gebruiken, wordt uitgelegd in [PSR-4][psr4], die zorgt voor een standaard bestand, class en namespace conventie die plug-and-play code mogelijk maakt.

In oktober 2014 heeft PHP-FIG de vorige autoloading-standaard als verouderd gemarkeerd: [PSR-0][psr0].
Zowel PSR-0 als PSR-4 zijn nog perfect bruikbaar. Het laatste vereist PHP 5.3 waardoor PHP 5.2 projecten PSR-0 implementeren.

Wanneer je gebruik wil maken van een autoloader standaard in een nieuwe applicatie of pakket kun je best PSR-4 bekijken.

* [Lees over Namespaces][namespaces]
* [Lees over PSR-0][psr0]
* [Lees over PSR-4][psr4]


[namespaces]: https://secure.php.net/language.namespaces
[psr0]: https://www.php-fig.org/psr/psr-0/
[psr4]: https://www.php-fig.org/psr/psr-4/
