---
isChild: true
title:   Costruire e pubblicare la tua applicazione
anchor:  building_and_deploying_your_application
---

## Costruire e pubblicare la tua applicazione {#building_and_deploying_your_application_title}

Se ti trovi a dover modificare lo schema del database o eseguire i test prima
dell'aggiornamento dei file manualmente, ripensaci! Con ogni compito manuale in
più che devi eseguire per pubblicare una nuova versione della tua applicazione
aumentano le possibilità di un errore fatale. Che tu stia gestendo un semplice
aggiornamento, un processo di build completo o una strategia di integrazione
continua, l'[automazione dello sviluppo][buildautomation] è tua amica.

Tra i compiti che potresti voler automatizzare ci sono:

* Gestione delle dipendenze
* Compilazione e minificazione dei media
* Esecuzione dei test
* Creazione di documentazione
* Pacchettizzazione
* Pubblicazione

### Strumenti di automazione dello sviluppo

Questi strumenti possono essere descritti come un insieme di script che
gestiscono compiti comuni nella pubblicazione del software. Lo strumento non è
parte del tuo software, ma agisce su di esso da 'fuori'.

Ci sono molti strumenti open source disponibili per aiutarti con l'automazione
dello sviluppo, alcuni scritti in PHP, altri no. Questo non dovrebbe impedirti
di usarli, se sono più adatti per uno specifico compito. Ecco alcuni esempi.

[Phing] è il modo più facile per iniziare con la pubblicazione automatica nel
mondo di PHP. Con Phing puoi controllare la pacchettizazione, la pubblicazione o
il processo di testing tramite un semplice file XML. Phing (che è basato su
[Apache Ant]) fornisce un ricco set di compiti solitamente richiesti per
installare o aggiornare un'applicazione Web e può essere esteso con compiti
personalizzati, scritti in PHP.

[Capistrano] è un sistema per *programmatori medio-avanzati* per eseguire
comandi in modo strutturato e ripetibile su una o più macchine remote. È pre-
configurato per la pubblicazione di applicazioni Ruby on Rails, ma molti lo
usano per **pubblicare applicazioni PHP**. Il suo corretto utilizzo dipende
dalla conoscenza di Ruby e Rake.

Il post [PHP Deployment with Capistrano][phpdeploy_capistrano] sul blog di Dave
Gardner è un buon punto d'inizio per programmatori PHP interessati a Capistrano.

[Chef] è più di un framework di pubblicazione. È un framework di integrazione di
sistema molto potente scritto in Ruby che non solo pubblica la tua applicazione
ma può costruire l'intero ambiente server o macchina virtuale.

[Deployer] è uno strumento di pubblicazione scritto in PHP; è semplice e
[funzionale. Esegue i compiti in parallelo, supporta la pubblicazione atomica,
[mantiene la consistenza tra i server. Ha ricette per compiti comuni relativi a
[Symfony, Laravel, Zend Framework e Yii.

#### Risorse Chef per sviluppatori PHP

* [Serie in tre parti sulla pubblicazione di un'applicazione LAMP con Chef, Vagrant ed EC2][chef_vagrant_and_ec2]
* [Articolo sull'installazione e la configurazione di PHP 5.3 e PEAR con Chef][Chef_cookbook]
* [Video tutorial su Chef][Chef_tutorial] fatto da Opscode, i creatori di Chef

#### Altre letture:

* [Automatizza il tuo progetto con Apache Ant][apache_ant_tutorial]

### Integrazione continua

> L'integrazione continua è una pratica di sviluppo software in cui i membri di
> un team integrano il loro lavoro frequentemente. Generalmente ogni persona
> integra il lavoro almeno giornalmente, portando a più integrazioni
> giornaliere. Molti team trovano che questo approccio riduca notevolmente i
> problemi di integrazione e permette a un team di sviluppare software coeso più
> rapidamente.

*-- Martin Fowler*

Ci sono diversi modi di implementare l'integrazione continua in PHP.
Recentemente [Travis CI] ha fatto un buon lavoro nel rendere l'integrazione
continua una realtà anche per piccoli progetti. Travis CI è un sistema hostato
di integrazione continua per la community open source. È integrato con GitHub e
offre supporto di prima classe per molti linguaggi, incluso PHP.

#### Altre letture:

* [Integrazione continua con Jenkins][Jenkins]
* [Integrazione continua con PHPCI][PHPCI]
* [Integrazione continua con Teamcity][Teamcity]

[buildautomation]: http://en.wikipedia.org/wiki/Build_automation
[Phing]: http://www.phing.info/
[Apache Ant]: http://ant.apache.org/
[Capistrano]: https://github.com/capistrano/capistrano/wiki
[phpdeploy_capistrano]: http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/
[Chef]: http://www.opscode.com/chef/
[chef_vagrant_and_ec2]: http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/
[Chef_cookbook]: https://github.com/opscode-cookbooks/php
[Chef_tutorial]: https://www.youtube.com/playlist?list=PLrmstJpucjzWKt1eWLv88ZFY4R1jW8amR
[apache_ant_tutorial]: http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/
[Travis CI]: https://travis-ci.org/
[Jenkins]: http://jenkins-ci.org/
[PHPCI]: http://www.phptesting.org/
[Teamcity]: http://www.jetbrains.com/teamcity/
[Deployer]: http://deployer.org/
