---
title:   Gebruikelijke mappenstructuur
isChild: true
anchor:  common_directory_structure
---

## Gebruikelijke mappenstructuur {#common_directory_structure_title}

Een gebruikelijke vraag bij diegene die starten met web ontwikkeling is, "waar plaats ik mijn code?". Door de jaren heen wordt deze vraag consistent beantwoord door "waar de `DocumentRoot` staat.". Dit antwoord is niet compleet, maar is wel een goede start.

Voor de veiligheid dienen configuratie bestanden niet in een map gezet te worden die door een bezoeker van een website beschikbaar is. Hierdoor worden publieke scripts in een publieke map gehouden en private configuraties en data wordt buiten deze map gehouden.

Voor elk team, CMS of framework waar men in werkt is een standaard mappenstructuur van toepassing.
Wanneer men echter een project alleen start is het kiezen van een structuur moeilijk.g.

[Paul M. Jones] heeft onderzoek gevoerd naar standaard mappen structuren van duizenden PHP Github projecten. Hij heeft een standaard bestands en mappensturtuur opgemaakt, de [Standard PHP Package Skeleton], gebaseerd op zijn onderzoek. In deze 
structuur zou de `DocumentRoot` moeten wijzen naar `public/`, unit tests in de `tests/` ma en externe libraries, zoals deze geinstalleerd door [composer], horen in de  `vendor/` map. Voor andere bestanden en mappen is het volgen van [Standard PHP Package Skeleton] interessant.

[Paul M. Jones]: https://twitter.com/pmjones
[Standard PHP Package Skeleton]: https://github.com/php-pds/skeleton
[Composer]: /#composer_and_packagist
