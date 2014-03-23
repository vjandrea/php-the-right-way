---
title:  Database
anchor: databases
---

# Database {#databases_title}

Molte volte il tuo codice PHP utilizzerà un database per memorizzare informazioni. Hai diverse opzioni per connetterti e
interagire con il tuo database. L'opzione consigliata _fino a PHP 5.1.0_ era di usare i driver nativi come [mysql][mysql],
[mysqli][mysqli], [pgsql][pgsql] etc.

I driver nativi vanno bene se usi UN SOLO database nella tua applicazione ma se, per esempio, stai usando MySQL e un po'
di MSSQL, o devi connetterti a un database Oracle, allora non potrai usare gli stessi driver. Dovrai imparare una nuova
API per ogni database e può diventare faticoso.

Inoltre, l'estensione mysql per PHP non è più in sviluppo attivo, ed è ufficialmente deprecata a partire da PHP 5.5, il
che significa che sarà rimossa nelle prossime release. Se stai usando `mysql_connect()` e `mysql_query()` nella tua
applicazione, dovrai riscriverla a un certo punto, quindi l'opzione migliore è sostituire mysql con mysqli o PDO nelle
tue applicazioni secondo la tua tabella di marcia, in modo da non avere fretta in futuro. _Se stai iniziando ora non
usare assolutamente l'estensione mysql: usa l'[estensione MySQLi][mysqli] o PDO._

* [PHP: Scegliere un'API per MySQL](http://php.net/manual/it/mysqlinfo.api.choosing.php)

## PDO

PDO è una libreria di astrazione della connessione al database integrata in PHP a partire dalla versione 5.1.0 che
fornisce un'interfaccia comune per dialogare con molti database differenti. PDO non tradurrà le query SQL e non emulerà
le funzionalità mancanti; è solo per la connessione a diversi tipi di database con la stessa API.

Ancora più importante è il fatto che `PDO` permette di iniettare in sicurezza input esterno (es. ID) nelle tue query SQL
senza doverti preoccupare di attacchi di tipo SQL injection. Questo è possibile tramite l'utilizzo dei PDO statement e
dei parametri.

Supponiamo che uno script PHP riceva un ID numerico come parametro query. Questo ID dev'essere usato per recuperare un
record utente dal database. Questo è il modo `sbagliato` di farlo:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

Questo è codice terribile. Stai inserendo un parametro grezzo nella tua query SQL. Il tuo script sarà manipolato in un
attimo. Immagina che un hacker passi un parametro `id` inventato chiamando un URL come
`http://dominio.com/?id=1%3BDELETE+FROM+users`. In questo modo la variabile `$_GET['id']` sarà impostata a `1;DELETE
FROM users`, che cancellerà tutti i tuoi utenti! Invece, dovresti sanitizzare l'input usando i parametri di PDO:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- Sanitizzato automaticamente da PDO
$stmt->execute();
{% endhighlight %}

Questo è codice corretto. Usa i parametri negli statement PDO. In questo modo viene eseguito l'escape dell'input esterno
ID prima che venga introdotto nel database prevenendo potenziali attacchi di tipo SQL injection.

* [Imparara a usare PDO][1]

Dovresti anche sapere che le connessioni al database usano risorse e non è raro che le risorse vengano esaurite se le
connessioni non sono chiuse implicitamente, ma questo è più comune in altri linguaggi. Utilizzando PDO puoi chiudere
implicitamente la connessione distruggendo l'oggetto e assicurandoti che tutti i rimanenti riferimenti a esso siano
cancellati (impostati a NULL). Se non lo fai esplicitamente, PHP chiuderà automaticamente la connessione quando il tuo
script termina l'esecuzione, a meno che, ovviamente, non usi le connessioni persistenti.


* [Impara a gestire le connessioni PDO][5]

## Livelli di astrazione

Molti framework forniscono il loro livello di astrazione che può essere costruito sulle spalle di PDO o meno. Spesso
questi emulano funzionalità di un database che un altro non fornisce racchiudendo le query in metodi PHP, fornendo una
reale astrazione del database. Ovviamente questo aggiunge un po' di fatica, ma se stai creando un'applicazione portabile
che deve lavorare con MySQL, PostgreSQL e SQLite un po' di fatica può essere spesa per del codice pulito.

Alcuni livelli di astrazione sono stati creati utilizzando gli standard di namespace [PSR-0][psr0] o [PSR-4][psr4] e
possono essere installati in qualunque applicazione desideri:

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]
* [ZF1 Db][3]

[1]: http://www.php.net/manual/it/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[3]: http://framework.zend.com/manual/it/zend.db.html
[4]: http://packages.zendframework.com/docs/latest/manual/it/index.html#zend-db
[5]: http://php.net/manual/it/pdo.connections.php
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/Propel/

[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
