---
isChild: true
title:   Composer e Packagist
anchor:  composer_and_packagist
---

## Composer e Packagist {#composer_and_packagist_title}

Composer è un **ottimo** gestore delle dipendenze per PHP. Elenca le dipendenze del tuo progetto in un file `composer.json`
e, con pochi semplici comandi, Composer scaricherà automaticamente le dipendenze e imposterà l'autoloading al posto tuo.

Ci sono già molte librerie PHP che sono compatibili con Composer pronte per essere usate nel tuo progetto. Questi "pacchetti"
sono elencati su [Packagist][1], il repository ufficiale per le librerie PHP disponibili tramite Composer.

### Come installare Composer

Puoi installare Composer localmente (nella tua directory di lavoro; ma questo non è più consigliato) o globalmente
(es. /usr/local/bin). Supponiamo tu lo voglia installare localmente. Dalla directory root del tuo progetto:

    curl -s https://getcomposer.org/installer | php

Questo scaricherà `composer.phar` (un archivio PHP binario). Puoi eseguirlo con `php` per gestire le dipendenze del tuo
progetto. <strong>Attenzione:</strong> se esegui direttamente del codice proveniente dal Web, controllalo online per
assicurarti che sia sicuro.

### Come installare Cmposer (manualmente)

L'installazione manuale di Composer è una tecnica avanzata; tuttavia, ci sono diverse ragioni per cui uno sviluppatore
potrebbe preferire questo metodo rispetto alla procedura di installazione interattiva. L'installazione interattiva controlla
la tua versione di PHP per assicurarsi che:

- una versione di PHP adatta sia in uso
- i file `.phar` possano essere eseguiti correttamente
- certe directory abbiano permessi sufficienti
- certe estensioni problematiche non siano caricate
- certe opzioni siano presenti nel `php.ini`

Poiché un'installazione manuale non esegue alcuno di questi controlli, dovrai decidere se il lavoro vale la pena. Ecco
come installare Composer manualmente:

    curl -s https://getcomposer.org/composer.phar -o $HOME/local/bin/composer
    chmod +x $HOME/local/bin/composer

La directory `$HOME/local/bin` (o una directory di tua scelta) dovrebbe essere nella variabile di ambiente `$PATH`. In
questo modo sarà disponibile un comando `composer`.

Quando incontri documentazione che dice di eseguire Composer con `php composer.phar install`, puoi sostituirlo con:

    composer install

This section will assume you have installed composer globally.

### Come definire e installare dipendenze

Composer tiene traccia delle dipendenze del tuo progetto in un file chiamato `composer.json`. Puoi gestirlo manualmente
se preferisci, o usare lo stesso Composer. Il comando `composer require` aggiunge una dipendenza del progetto e,
se non hai un file `composer.json`, lo crea. Ecco un esempio che aggiunge [Twig][2] come dipendenza del tuo progetto:

	composer require twig/twig:~1.8

In alternativa puoi usare il comando `composer init`, che ti guiderà nella creazione di un file `composer.json`
per il tuo progetto. In ogni caso, una volta che hai creato il file `composer.json`, puoi dire a Composer di scaricare e
installare le dipendenze nella cartella `vendors/`. Questo vale anche per i progetti che hai scaricato e che forniscono
un file `composer.json`:

    composer install

Adesso, aggiungi questa linea al file principale della tua applicazione PHP; questo dirà a PHP di usare l'autoloader di
Composer per le dipendenze del tuo progetto.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Ora puoi usare le dipendenze del tuo progetto, che saranno caricate automaticamente quando richieste.

### Aggiornare le dipendenze

Composer crea un file chiamato `composer.lock` che contiene la versione esatta di ogni pacchetto che ha scaricato durante
l'esecuzione di `php composer.phar install`. Se condividi il tuo progetto con altre persone e il file `composer.lock` è
parte della distribuzione, quando eseguiranno `php composer.phar install` otterranno le tue stesse versioni. Per aggiornare
le dipendenze, esegui `php composer.phar update`.

Questo è particolarmente utile quando definisci i tuoi requisiti di versione in maniera flessibile. Per esempio, un requisito
di ~1.8 significa "qualunque versione dopo la 1.8.0, ma minore di 2.0.x-dev". Puoi anche usare il carattere jolly `*` (.es
`1.8.*`). Ora il comando `php composer.phar update` aggiornerà le dipendenze alla versione più recente che soddisfa i requisiti
definiti.

### Notifiche di aggiornamento

Per ricevere notifiche riguardo release di nuove versioni puoi registrati a [VersionEye][3], un servizio web che può
monitorare i tuoi account GitHub e BitBucket alla ricerca di file `composer.json` e mandare email con le nuove release
dei pacchetti.

### Controllare la presenza di vulnerabilità nelle tue dipendenze

Il [Security Advisories Checker][3] è un web service e uno strumento da linea di comando. Entrambi esamineranno il file
`composer.lock` e ti diranno se devi aggiornare le tue dipendenze.

* [Impara a usare Composer][4]

[1]: http://packagist.org/
[2]: http://twig.sensiolabs.org
[3]: https://www.versioneye.com/
[4]: https://security.sensiolabs.org/
[5]: http://getcomposer.org/doc/00-intro.md
