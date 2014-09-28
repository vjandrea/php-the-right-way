---
isChild: true
title:   Configurazione Mac
anchor:  mac_setup
---

## Configurazione Mac  {#mac_setup_title}

OS X viene fornito con una versione pre-pacchettizzata di PHP, ma è normalmente
un po' più vecchia dell'ultima versione stabile. Mountain Lion ha la 5.3.10,
Mavericks ha la 5.4.17 e Yosemite ha la 5.5.9, ma con PHP 5.6 già rilasciato di
solito non è abbastanza.

Ci sono diversi modi per installare PHP su OS X.

### Installare PHP tramite Homebrew

[Homebrew](http://brew.sh) è un potente gestore di pacchetti per OS X che può
aiutarti a installare facilmente PHP e varie estensioni. [Homebrew PHP] è un
repository che contiene "formule" per Homebrew relative a PHP e ti permetterà
di installare PHP.

A questo punto, puoi installare `php53`, `php54`, `php55` o `php56` usando il
comando `brew install` e cambiando la versione attiva modificando la variabile
`PATH`.

### Installare PHP tramite phpbrew
[phpbrew] è uno strumento per l'installazione e la gestione di versioni multiple
di PHP. Può essere molto utile se due applicazioni/progetti differenti
richiedono versioni differenti di PHP e non stai usando le macchine virtuali.

### Compilare il sorgente

Un'altra opzione che ti fornisce controllo sulla versione di PHP che installi è
[compilarlo tu stesso][mac-compile]. In questo caso assicurati di avere
installato XCode o il sostituto di Apple ["Strumenti da riga di comando per XCode"],
scaricabile dal Centro Sviluppatori Mac di Apple.

### Installatori all-in-one

Le soluzioni listate sopra gestiscono principalmente solo PHP, e non forniscono
cose come Apache, Nginx o un server SQL. Le soluzioni "all-in-one" come [MAMP][mamp-downloads]
e [XAMPP][xampp] installeranno questi altri software per te e li integreranno
l'uno con l'altro, ma la facilità d'installazione compromette la flessibilità.

[Homebrew]: http://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[mac-compile]: http://www.php.net/manual/en/install.macosx.compile.php
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Strumenti da riga di comando per XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/
[phpbrew]: https://github.com/phpbrew/phpbrew
[xampp]: http://www.apachefriends.org/en/xampp.html
