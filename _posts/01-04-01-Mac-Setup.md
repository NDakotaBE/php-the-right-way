---
title: Installatie (macOS)
isChild: true
anchor:  mac_setup
---

## Installatie op macOS {#mac_setup_title}

macOS komt met PHP geïnstalleerd, maar deze is meestal een lagere versie dan de laatste stabiele release. Er zijn meerdere
manieren om de laatste versie van PHP te installeren op macOS.

### Installeer PHP via Homebrew

[Homebrew] is een package manager voor macOS die je helpt om gemakkelijk PHP te installereren samen met verschillende extensies.
De Homebrew code repository voorziet "formules" voor PHP 5.6, 7.0, 7.1 en 7.2. Installeer de laatste versie met het commando:

```
brew install php@7.2
```

Je kunt veranderen van Homebrew PHP versies door je `PATH` variabele aan te passen. Een andere alternatief is om [brew-php-switcher][brew-php-switcher] te gebruiken en zo automatisch te veranderen van PHP versie.

### Installeer PHP via MacPorts

Het [MacPorts] Project is een initiatief van de open-source community om een gemakkelijk te gebruiken systeem te ontwikkelen om het compileren, instaleren en upgraden van op command-line, X11 of Aqua gebaseerde opensource software op het OS X OS.

MacPorts ondersteund voorgecompileerde binaries, opdat je niet elke dependency dien te hercompileren van de bronbestanden.
Het maakt het vooral gemakkelijkals je geen enkel pakket op je systeem geinstalleerd hebt..

Op dit moment kun je `php54`, `php55`, `php56`, `php70` of `php71` installeren door het commando `port install` te gebruiken.
Bijvoorbeeld:

    sudo port install php56
    sudo port install php71

Je kan ook het commando `select` gebruiken om je actieve PHP versie te veranderen:

    sudo port select --set php php71

### Installeer PHP via phpbrew

[phpbrew] is een tool om meerder versies van PHP te installeren en te configureren. Dit is vooral gemakkelijk wanneer je 
meerdere applicaties/projecten hebt, waar je verschillende PHP versies voor nodig hebt, zonder gebruik te maken van virtuele machines.

### Installeer PHP via Liip's binary installer

Een andere populaire optie is [php-osx.liip.ch]. Deze voorziet een installatie methode waar maar 1 commando voor nodig is.
Deze optie laat je toe om PHP versies van 5.3 tot 7.3 te installeren. 
Het vervangt de PHP binaries, die standaard door Apple geinstalleerd zijn niet, maar installeert alles op een aparte locatie 
[/usr/local/php5]

### Compileren van de broncode

Een andere optie, dewelke je meer controle geeft over de versie van PHP die je installeert, is om [ze zelf te compileren][mac-compile].
In dit geval, moet je er zeker voor zorgen dat je ofwel, [Xcode][xcode-gcc-substitution] of Apple's vervanging
["Command Line Tools for XCode"] geinstalleerd hebt.

### All-in-One Installers

De bovengenoemde oplossingen voorzien meestal PHP zelf en zorgen niet voor zaken zoals Apache, Nginx of een SQL server.
"All-in-one" oplossingen zoals [MAMP][mamp-downloads] en [XAMPP][xampp] zullen deze andere software paketten installeren voor je
en deze allemaal samenbrengen.
Dit heeft natuurlijk als nadeel dat flexibiliteit hier in het gedrang kan komen.

[Homebrew]: https://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: https://php-osx.liip.ch/
[mac-compile]: https://secure.php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: https://www.mamp.info/en/downloads/
[xampp]: https://www.apachefriends.org/index.html
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
