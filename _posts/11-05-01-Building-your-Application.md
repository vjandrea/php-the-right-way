---
isChild: true
title:   Costruire e pubblicare la tua applicazione
anchor:  building_and_deploying_your_application

## Costruire e pubblicare la tua applicazione {#costruire_e_pubblicare_la_tua_applicazione_title}

Se ti trovi a dover modificare lo schema del database o eseguire i test prima dell'aggiornamento dei file manualmente,
ripensaci! Con ogni compito manuale in più che devi eseguire per pubblicare una nuova versione della tua applicazione
aumentano le possibilità di un errore fatale. Che tu stia gestendo un semplice aggiornamento, un processo di build
completo o una strategia di integrazione continua,
l'[automazione dello sviluppo](http://it.wikipedia.org/wiki/Automazione_dello_sviluppo) è tua amica.

Tra i compiti che potresti voler automatizzare ci sono:

* Gestione delle dipendenze
* Compilazione e minificazione dei media
* Esecuzione dei test
* Creazione di documentazione
* Pacchettizzazione
* Pubblicazione

### Strumenti di automazione dello sviluppo

Questi strumenti possono essere descritti come un insieme di script che gestiscono compiti comuni nella pubblicazione
del software. Lo strumento non è parte del tuo software, ma agisce su di esso da 'fuori'.

Ci sono molti strumenti open source disponibili per aiutarti con l'automazione dello sviluppo, alcuni scritti in PHP,
altri no. Questo non dovrebbe impedirti di usarli, se sono più adatti per uno specifico compito. Ecco alcuni esempi.

[Phing](http://www.phing.info/) è il modo più facile per iniziare con la pubblicazione automatica nel mondo di PHP. Con
Phing puoi controllare la pacchettizazione, la pubblicazione o il processo di testing tramite un semplice file XML. Phing
(che è basato su [Apache Ant](http://ant.apache.org)) fornisce un ricco set di compiti solitamente richiesti per installare
o aggiornare un'applicazione Web e può essere esteso con compiti personalizzati, scritti in PHP.

[Capistrano](https://github.com/capistrano/capistrano/wiki) è un sistema per *programmatori medio-avanzati* per eseguire
comandi in modo strutturato e ripetibile su una o più macchine remote. È pre-configurato per la pubblicazione di applicazioni
Ruby on Rails, ma molti lo usano per **pubblicare applicazioni PHP**. Il suo corretto utilizzo dipende dalla conoscenza
di Ruby e Rake.

Il post [PHP Deployment with Capistrano](http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/)
sul blog di Dave Gardner è un buon punto d'inizio per programmatori PHP interessati a Capistrano.

[Chef](http://www.opscode.com/chef/) è più di un framework di pubblicazione. È un framework di integrazione di sistema
molto potente scritto in Ruby che non solo pubblica la tua applicazione ma può costruire l'intero ambiente server o
macchina virtuale.

Alcune risorse su Chef e PHP:

* [Serie in tre parti sulla pubblicazione di un'applicazione LAMP con Chef, Vagrant ed EC2](http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/)
* [Articolo sull'installazione e la configurazione di PHP 5.3 e PEAR con Chef](https://github.com/opscode-cookbooks/php)

Altre letture:

* [Automatizza il tuo progetto con Apache Ant](http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/)
* [Maven](http://maven.apache.org/), un framework di sviluppo basato su Ant e [come usarlo con PHP](http://www.php-maven.org/)

### Integrazione continua

> Continuous Integration is a software development practice where members of a > team integrate their work frequently,
> usually each person integrates at least daily — leading to multiple  integrations per day. Many teams find that this
> approach leads to significantly reduced integration problems and allows a team to develop cohesive software more
> rapidly.

> L'integrazione continua è una pratica di sviluppo software in cui i membri di un team integrano il loro lavoro
> frequentemente. Generalmente ogni persona integra il lavoro almeno giornalmente, portando a più integrazioni giornaliere.
> Molti team trovano che questo approccio riduca notevolmente i problemi di integrazione e permette a un team di sviluppare
> software coeso più rapidamente.

*-- Martin Fowler*

Ci sono diversi modi di implementare l'integrazione continua in PHP. Recentemente [Travis CI](https://travis-ci.org/) ha
fatto un buon lavoro nel rendere l'integrazione continua una realtà anche per piccoli progetti. Travis CI è un sistema di
integrazione continua per la community open source. È integrato con GitHub e offre supporto di prima classe per molti
linguaggi, incluso PHP.

Altre letture:

* [Integrazione continua con Jenkins](http://jenkins-ci.org/)
* [Integrazione continua con PHPCI](http://www.phptesting.org/)
* [Integrazione continua con Teamcity](http://www.jetbrains.com/teamcity/)
