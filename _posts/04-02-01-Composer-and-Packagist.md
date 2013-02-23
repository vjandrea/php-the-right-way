---
isChild: true
title:   Composer e Packagist
---

## Composer e Packagist {#composer_e_packagist_title}

Composer è un **ottimo** gestore delle dipendenze per PHP. Elenca le dipendenze
del tuo progetto in un file `composer.json` e, con pochi semplici comandi,
Composer scaricherà automaticamente le dipendenze e imposterà l'autoloading al
posto tuo.

Ci sono già molte librerie PHP che sono compatibili con Composer pronte per
essere usate nel tuo progetto. Questi "pacchetti" sono elencati su
[Packagist][1], il repository ufficiale per le librerie PHP disponibili tramite
Composer.

### Come installare Composer

Puoi installare Composer localmente (nella tua directory di lavoro; ma questo
non è più consigliato) o globalmente (es. /usr/local/bin). Supponiamo tu lo
voglia installare localmente. Dalla directory root del tuo progetto:

    curl -s https://getcomposer.org/installer | php

Questo scaricherà `composer.phar` (un archivio PHP binario). Puoi eseguirlo con
`php` per gestire le dipendenze del tuo progetto. <strong>Attenzione:</strong>
se esegui del codice proveniente dal Web direttamente, controllalo online per
assicurarti che sia sicuro.

### Come installare Cmposer (manualmente)

L'installazione manuale di Composer è una tecnica avanzata; tuttavia, ci sono
diverse ragioni per cui uno sviluppatore potrebbe preferire questo metodo invece
della procedura d'installazione interattiva. L'installazione interattiva
controlla la tua installazione di PHP per assicurarsi che:

- una versione di PHP adatta sia in uso
- i file `.phar` possano essere eseguiti correttamente
- certe directory abbiano permessi sufficienti
- certe estensioni problematiche non siano caricate
- certe opzioni siano presenti nel `php.ini`

Poiché un'installazione manuale non esegue alcuno di questi controlli, dovrai
decidere se il lavoro vale la pena. Ecco come installare Composer manualmente:

    curl -s https://getcomposer.org/composer.phar -o $HOME/local/bin/composer
    chmod +x $HOME/local/bin/composer

La directory `$HOME/local/bin` (o una directory di tua scelta) dovrebbe essere
nella variabile di ambiente `$PATH`. In questo modo sarà disponibile un comando
`composer`.

Quando incontri documentazione che dice di eseguire Composer con `php
composer.phar install`, puoi sostituirlo con:

    composer install

### Come definire e installare dipendenze

Per prima cosa, crea un file `composer.json` nella stessa directory di
`composer.phar`. Ecco un esempio che elenca [Twig][2] come dipendenza del
progetto:

	{
	    "require": {
	        "twig/twig": "1.8.*"
	    }
	}

Successivamente, esegui questo comando dalla root del tuo progetto:

    php composer.phar install

Questo scaricherà e installerà le dipendenze del progetto nella cartella
`vendor/`. Dopodiché, aggiungi questa linea al file PHP principale della tua
applicazione; questo dirà a PHP di usare l'autoloader di Composer per le
dipendenze del tuo progetto.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Ora puoi usare le dipendenze del tuo progetto, che saranno caricate
automaticamente quando richieste.

* [Impara a usare Composer][3]

[1]: http://packagist.org/
[2]: http://twig.sensiolabs.org
[3]: http://getcomposer.org/doc/00-intro.md
