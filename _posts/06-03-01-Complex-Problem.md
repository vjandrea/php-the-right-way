---
isChild: true
title:   Problema complesso
anchor:  complex_problem
---

## Problema complesso {#problema_complesso_title}

Se hai mai letto qualcosa sull'iniezione delle dipendenze allora hai probabilmente visto i termini
*"Inversione del controllo"* o *"Principio di inversione della dipendenza"*. Questi sono problemi complessi risolti
dall'iniezione delle dipendenze.

### Inversione del controllo

L'inversione del controllo consiste, come suggerisce il nome, nell'"invertire il controllo" di un sistema tenendo il
controllo organizzativo completamente separato dai nostri oggetti. Con l'iniezione delle dipendenze, questo significa
rendere le dipendenze più flessibili controllandole e istanziandole in un altro punto del sistema.

Per anni, i framework PHP hanno usato l'inversione del controllo. Tuttavia, la domanda è diventata: quale parte del
controllo stai invertendo, e dove? Per esempio, i framework MVC generalmente fornivano un oggetto padre o un controller
di base che gli altri controller dovevano estendere per accedere alle sue dipendenze. Questa **è** inversione del
controllo, ma invece di rendere le dipendenze più flessibili, questo metodo semplicemente le spostava.

L'iniezione delle dipendenze ci permette di risolvere questo problema in maniera più elegante, iniettando solo le
dipendenze che ci servono, quando ci servono, senza il bisogno di alcuna dipendenza cablate a codice.

### Principio di inversione della dipendenza

Il principio di inversione della dipendenza è la "D" nell'insieme di principi di design orientato agli oggetti
S.O.L.I.D., secondo cui si dovrebbe *"Dipendere dalle astrazioni. Non dipendere dalle concrezioni."* Detto
semplicemente, questo significa che le nostre dipendenze dovrebbero essere interfacce/contratti o classi astratte, non
implementazioni concrete. Possiamo facilmente rifattorizzare l'esempio sopra in modo che segua questo principio.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(AdapterInterface $adapter)
    {
        $this->adapter = $adapter;
    }
}

interface AdapterInterface {}

class MysqlAdapter implements AdapterInterface {}
{% endhighlight %}

Ci sono diversi benefici all'approccio seguito, in cui la classe `Database` dipende ora da un'interfaccia piuttosto che
da un'implementazione concreta.

Pensa di lavorare in team, e che un collega stia lavorando all'adattatore. Nel nostro primo esempio, avremmo dovuto
aspettare che tale collega finisse l'adattore prima di poterlo imitare appropriatamente per i nostri unit test. Ora che
la dipendenza è un'interfaccia/contratto, possiamo felicemente imitare quell'interfaccia sapendo che il nostro collega
costruirà l'adattatore basandosi su quel contratto.

Un beneficio ancora più grande è che ora il nostro codice è molto più scalabile. Se tra un anno decidiamo che vogliamo
migrare verso un tipo diverso di database, possiamo scrivere un adattatore che implementi l'interfaccia originale e
iniettare quello. Non servirebbe alcun'altra rifattorizzazione, perché saremmo sicuri che l'adattore segue il contratto
stabilito dall'interfaccia.
