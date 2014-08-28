---
isChild: true
title: Livelli di astrazione
anchor: databases_abstraction_layers
---

## Livelli di astrazione {#databases_abstraction_layers_title}

Molti framework forniscono il loro livello di astrazione che può essere costruito sulle spalle di PDO o meno. Spesso
questi emulano funzionalità di un database che un altro non fornisce racchiudendo le query in metodi PHP, fornendo una
reale astrazione del database invece della semplice astrazione della connessione che offre PDO.. Ovviamente questo
aggiunge un po' di fatica, ma se stai creando un'applicazione portabile che deve lavorare con MySQL, PostgreSQL e SQLite
un po' di fatica può essere spesa per del codice pulito.

Alcuni livelli di astrazione sono stati creati utilizzando gli standard di namespace [PSR-0][psr0] o [PSR-4][psr4] e
possono essere installati in qualunque applicazione desideri:

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]

[1]: http://www.php.net/manual/it/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[4]: http://packages.zendframework.com/docs/latest/manual/it/index.html#zend-db
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/

[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
