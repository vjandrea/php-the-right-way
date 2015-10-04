---
isChild: true
title:   Configurazione Mac
anchor:  mac_setup
---

## Configurazione Mac  {#mac_setup_title}

OS X viene fornito con una versione pre-pacchettizzata di PHP, ma è normalmente
un po' più vecchia dell'ultima versione stabile. Mountain Lion ha la 5.3.10,
Mavericks ha la 5.4.17 e Yosemite ha la 5.5.9, ma con PHP 5.6 già rilasciato di
solito è meglio aggiornare.

Ci sono diversi modi per installare PHP su OS X.

### Installare PHP tramite Homebrew

[Homebrew](http://brew.sh) è un potente gestore di pacchetti per OS X che può
aiutarti a installare facilmente PHP e varie estensioni. [Homebrew PHP] è un
repository che contiene "formule" per Homebrew relative a PHP e ti permetterà
di installare PHP.

A questo punto, puoi installare `php53`, `php54`, `php55` o `php56` usando il
comando `brew install` e cambiando la versione attiva modificando la variabile
`PATH`.

### Installare PHP tramite Macports

Il progetto [MacPorts] è un'iniziativa della comunità open source per il design
di un sistema di semplice utilizzo per la compilazione, l'installazione e
l'aggiornamento di software open source per linea di comando, X11 o Acqua sul
sistema operativo OS X.

MacPorts supporta i binari precompilati, quindi non devi ricompilare le
dipendenze dai sorgenti ogni volta. È un salvavita se non hai alcun pacchetto
installato sul sistema.

In questo momento puoi installare `php53`, `php54`, `php55` o `php56` usando il
comando `port install`. Per esempio:

    sudo port install php54
    sudo port install php55

E puoi eseguire il comando `select` per cambiare la versione attiva di PHP:

    sudo port select --set php php55

### Installare PHP tramite phpbrew

[phpbrew] è uno strumento per l'installazione e la gestione di versioni multiple
di PHP. Può essere molto utile se due applicazioni/progetti differenti
richiedono versioni differenti di PHP e non stai usando le macchine virtuali.

### Compilare il sorgente

Un'altra opzione che ti fornisce controllo sulla versione di PHP che installi è
[compilarlo tu stesso][mac-compile]. In questo caso assicurati di avere
installato [Xcode][xcode-gcc-substitution] o il sostituto di Apple
["Strumenti da riga di comando per XCode"], scaricabile dal Centro Sviluppatori
Mac di Apple.

### Installatori all-in-one

Le soluzioni elencate sopra gestiscono principalmente solo PHP, e non forniscono
cose come Apache, Nginx o un server SQL. Le soluzioni "all-in-one" come [MAMP][mamp-downloads]
e [XAMPP][xampp] installeranno questi altri software per te e li integreranno
l'uno con l'altro, ma la facilità d'installazione compromette la flessibilità.

[Homebrew]: http://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[mac-compile]: http://php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Strumenti da riga di comando per XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/
[xampp]: http://www.apachefriends.org/en/xampp.html
