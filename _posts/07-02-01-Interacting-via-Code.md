---
isChild: true
title:  Interagire coi database
anchor: databases_interacting
---

## Interagire coi database {#databases_interacting_title}

Quando gli sviluppatori iniziano a imparare PHP, spesso finiscono per mescolare l'interazion col database con la logica
di presentazione, usando codice come questo:

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
?>
</ul>
{% endhighlight %}

Questo è una pessima pratica per diverse ragioni: principalmente è difficile da debuggare, difficile da testare,
difficile da leggere e stamperà molti campi se non imposti un limite.

Nonostante ci siano molte soluzioni per farlo - a seconda che si preferisca l'[OOP](/#object-oriented-programming) o la
[programmazione funzionale](/#functional-programming) - ci dev'essere un elemento di separazione.

Considera il passo più semplice:

{% highlight php %}
<?php
function getAllFoos($db) {
    return $db->query('SELECT * FROM table');
}

foreach (getAllFoos($db) as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // BAD!!
}
{% endhighlight %}

Questo è un buon inizio. Metti quei due pezzi in due file diversi e hai una separazione pulita.

Crea una classe per metterci quel metodo e hai un "modello". Crea un semplice file `.php` per metterci la logica di
presentazione e hai una "vista", che è molto simile all'[MVC] - un'architettura OOP comune a molti
[framework](#frameworks_title).

**foo.php**

{% highlight php %}
<?php

$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8', 'username', 'password');

// Rendi disponibile il tuo modello
include 'models/FooModel.php';

// Crea un'istanza
$fooList = new FooModel($db);

// Mostra una vista
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class Foo()
{
    protected $db;

    public function __construct(PDO $db)
    {
        $this->db = $db;
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<? foreach ($fooList as $row): ?>
    <?= $row['field1'] ?> - <?= $row['field1'] ?>
<? endforeach ?>
{% endhighlight %}

Questa è essenzialmente la stessa cosa che fanno molti framework moderni, anche se un po' più manuale. Potresti non
averne sempre bisogno, ma mischiare insieme troppa logica di presentazione e interazione col database può essere un
problema serio se vorrai mai fare lo [unit testing](/#unit-testing) della tua applicazione.

[PHPBridge] ha un'ottima risorsa chiamata [Creating a Data Class] che copre un argomento simile, ed è perfetta per
sviluppatori che stanno familiarizzando solo ora col concetto di interazione coi database.

[MVC]: http://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488
[PHPBridge]: http://phpbridge.org/
[Creating a Data Class]: http://phpbridge.org/intro-to-php/creating_a_data_class
