---
title:  Database
anchor: databases
---

# Database {#databases_title}

Molte volte il tuo codice PHP utilizzerà un database per memorizzare
informazioni. Hai diverse opzioni per connetterti e interagire con il tuo
database. L'opzione consigliata **fino a PHP 5.1.0** era di usare i driver
nativi come [mysqli], [pgsql], [mssql] etc.

I driver nativi vanno bene se usi _un_ database nella tua applicazione ma se,
per esempio, stai usando MySQL e un po' di MSSQL, o devi connetterti a un
database Oracle, allora non potrai usare gli stessi driver. Dovrai imparare una
nuova API per ogni database e può diventare faticoso.

## Estensione MySQL

Inoltre, l'estensione [mysql] per PHP non è più in sviluppo attivo, ed è
[ufficialmente deprecata a partire da PHP 5.5.0](officially deprecated as of PHP 5.5.0),
 il che significa che sarà rimossa nelle prossime release. Se stai usando
funzioni che iniziano con `mysql_*` come `mysql_connect()` e `mysql_query()`
nella tua applicazione, semplicemente non saranno disponibili nelle prossime
versioni di PHP. Questo significa che dovrai riscrivere l'applicazione a un
certo punto, quindi l'opzione migliore è sostituire mysql con [mysqli] o [PDO]
nelle tue applicazioni secondo la tua tabella di marcia, in modo da non avere
fretta in futuro.

**Se stai iniziando ora non usare assolutamente l'estensione [mysql]: usa
l'[estensione MySQLi](mysqli) o usa PDO.**

* [PHP: Scegliere un'API per MySQL](http://php.net/manual/it/mysqlinfo.api.choosing.php)
* [PDO Tutorial for MySQL Developers](http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers)

## Estensione PDO

PDO è una libreria di astrazione della connessione al database &mdash; integrata
in PHP dalla 5.1.0 &mdash; che fornisce un'interfaccia comune per dialogare con
molti database differenti. Per esempio, puoi usare lo stesso codice per
interfacciarti con MySQL o SQLite:

{% highlight php %}
// PDO + MySQL
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');
$statement = $pdo->query("SELECT some\_field FROM some\_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);

// PDO + SQLite
$pdo = new PDO('sqlite:/path/db/foo.sqlite');
$statement = $pdo->query("SELECT some\_field FROM some\_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);
{% endhighlight %}

PDO non tradurrà le query SQL e non emulerà le funzionalità mancanti; è solo per
la connessione a diversi tipi di database con la stessa API.

Ancora più importante è il fatto che `PDO` permette di iniettare in sicurezza
input esterno (es. ID) nelle tue query SQL senza doverti preoccupare di attacchi
di tipo SQL injection. Questo è possibile tramite l'utilizzo dei PDO statement e
dei parametri.

Supponiamo che uno script PHP riceva un ID numerico come parametro query. Questo
ID dev'essere usato per recuperare un record utente dal database. Questo è il
modo `sbagliato` di farlo:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

Questo è codice terribile. Stai inserendo un parametro grezzo nella tua query
SQL. Il tuo script sarà manipolato in un attimo usando una pratica chiamata [SQL
Injection](http://wiki.hashphp.org/Validation). Immagina che un hacker passi un
parametro `id` inventato chiamando un URL come
`http://dominio.com/?id=1%3BDELETE+FROM+users`. In questo modo la variabile
`$_GET['id']` sarà impostata a `1;DELETE FROM users`, che cancellerà tutti i
tuoi utenti! Invece, dovresti sanitizzare l'input usando i parametri di PDO:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- Sanitizzato automaticamente da PDO
$stmt->execute();
{% endhighlight %}

Questo è codice corretto. Usa i parametri negli statement PDO. In questo modo
viene eseguito l'escape dell'input esterno ID prima che venga introdotto nel
database prevenendo potenziali attacchi di tipo SQL injection.

* [Impara a usare PDO](Learn about PDO)

Dovresti anche sapere che le connessioni al database usano risorse e non è raro
che le risorse vengano esaurite se le connessioni non sono chiuse
implicitamente, ma questo è più comune in altri linguaggi. Utilizzando PDO puoi
chiudere implicitamente la connessione distruggendo l'oggetto e assicurandoti
che tutti i rimanenti riferimenti a esso siano cancellati (impostati a NULL). Se
non lo fai esplicitamente, PHP chiuderà automaticamente la connessione quando il
tuo script termina l'esecuzione, a meno che, ovviamente, non usi le connessioni
persistenti.

* [Impara a usare le connessioni PDO](Learn about PDO connections)

[Learn about PDO]: http://www.php.net/manual/en/book.pdo.php
[Learn about PDO connections]: http://php.net/manual/en/pdo.connections.php
[officially deprecated as of PHP 5.5.0]: http://php.net/manual/en/migration55.deprecated.php

[pdo]: http://php.net/pdo
[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
[mssql]: http://php.net/mssql
