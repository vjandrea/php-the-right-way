---
layout: page
title: Design Pattern
---

# Design Pattern

Ci sono diversi modi di strutturare il codice e il progetto per la tua applicazione Web, e puoi sforzarti quanto preferisci nell'architettarli. Generalmente, però, è una buona idea seguire dei modelli comuni, in modo da rendere il tuo codice più
semplice da gestire per te e più facile da leggere per gli altri.

* [Modelli architetturali su Wikipedia](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Design pattern su Wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)

## Factory

Uno dei design pattern più usati è il _Factory Method_. In questo pattern, una classe crea l'oggetto che vuoi utilizzare.
Considera il seguente esempio di _Factory Method_:

{% highlight php %}
<?php
class Automobile
{
    private $vehicle_make;
    private $vehicle_model;

    public function __construct($make, $model)
    {
        $this->vehicle_make = $make;
        $this->vehicle_model = $model;
    }

    public function get_make_and_model()
    {
        return $this->vehicle_make . ' ' . $this->vehicle_model;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// facciamo creare l'oggetto Automobile alla factory
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->get_make_and_model()); // visualizza "Bugatti Veyron"
{% endhighlight %}

Questo codice usa una _factory_ per creare l'oggetto Automobile. Ci sono due potenziali benefici nello strutturare il
codice in questo modo. Il primo è che, se in futuro avrai bisogno di rinominare, modificare o sostituire la classe
Automobile, dovrai solamente modificare la _factory_ invece di ogni riga del tuo codice che usa la classe Automobile. Il
secondo beneficio è che, se creare un oggetto è un lavoro complicato, puoi fare tutto nella _factory_ invece di ripeterlo
ogni volta che vuoi creare una nuova  istanza.

Usare il _Factory Method_ non è sempre necessario (né saggio). Il codice di esempio mostrato qui è così semplice che
aggiungere una _factory_ significa solo complicare inutilmente l'applicazione. Tuttavia, se stai creando un progetto
grande o complesso, potresti volerti risparmiare molta fatica usando le _factory_.


* [Factory Method su Wikipedia](https://it.wikipedia.org/wiki/Factory_method)

## Singleton

Durante la progettazione di un'applicazione Web, è spesso sensato concettualmente e architetturalmente permettere
l'accesso a una e una sola istanza di una specifica classe. Il pattern _singleton_ ci permette di fare ciò.

{% highlight php %}
<?php
class Singleton
{
    /**
     * Returns the *Singleton* instance of this class.
     *
     * @staticvar Singleton $instance The *Singleton* instances of this class.
     *
     * @return Singleton The *Singleton* instance.
     */
    public static function getInstance()
    {
        static $instance = null;
        if (null === $instance) {
            $instance = new static();
        }

        return $instance;
    }

    /**
     * Protected constructor to prevent creating a new instance of the
     * *Singleton* via the `new` operator from outside of this class.
     */
    protected function __construct()
    {
    }

    /**
     * Private clone method to prevent cloning of the instance of the
     * *Singleton* instance.
     *
     * @return void
     */
    private function __clone()
    {
    }

    /**
     * Private unserialize method to prevent unserializing of the *Singleton*
     * instance.
     *
     * @return void
     */
    private function __wakeup()
    {
    }
}

class SingletonChild extends Singleton
{
}

$obj = Singleton::getInstance();
var_dump($obj === Singleton::getInstance());             // bool(true)

$anotherObj = SingletonChild::getInstance();
var_dump($anotherObj === Singleton::getInstance());      // bool(false)

var_dump($anotherObj === SingletonChild::getInstance()); // bool(true)
{% endhighlight %}

Il codice qui sopra implementa il pattern singleton usando una
[variabile *statica*](http://php.net/language.variables.scope#language.variables.scope.static) e il metodo statico di
creazione `getInstance()`.

Nota che:

* Il costruttore [`__construct`](http://php.net/language.oop5.decon#object.construct) è dichiarato protetto per impedire
la creazione di una nuova istanza fuori dalla classe tramite l'operatore `new`.
* Il metodo magico [`__clone`](http://php.net/language.oop5.cloning#object.clone) è dichiarato privato per impedire la
clonazione di un'istanza della classe tramite l'operatore [`clone`](http://php.net/language.oop5.cloning).
* Il metodo magico [`__wakeup`](http://php.net/language.oop5.magic#object.wakeup) è dichiarato privato per impedire la
deserializzazione di un'istanza della classe tramite la funzione globale [`unserialize()`](http://php.net/function.unserialize).
* Una nuova istanza è creata tramite [binding statico dinamico](http://php.net/language.oop5.late-static-bindings) nel
metodo statico di creazione `getInstance()` con la parole chiave `static`. Questo permette di estendere la classe di esempio
`Singleton`.

Il pattern singleton è utile quando dobbiamo assicurarci di avere una singola istanza di una classe per l'intero ciclo
di vita della richiesta. Questo succede solitamente quando abbiamo oggetti globali (come una classe Configuration) o
una risorsa condivisa (come una coda degli eventi).

Dovresti fare attenzione nell'utilizzo del pattern singleton, poiché per sua natura introduce uno stato globale nella
tua applicazione, riducendo la testabilità. Nella maggior parte dei casi l'iniezione delle dipendenze può (e deve)
essere usata invece di una classe singleton. Utilizzare l'iniezione delle dipendenze significa evitare di introdurre
legami inutili nel design della nostra applicazione, giacchè l'oggetto che utilizza la risorsa condivisa o globale non
richiede la conoscenza di una classe concretamente definita.

>>>>>>> upstream/gh-pages

* [Singleton su Wikipedia](https://it.wikipedia.org/wiki/Singleton)

## Strategy

With the strategy pattern you encapsulate specific families of algorithms allowing the client class responsible for 
instantiating a particular algorithm to have no knowledge of the actual implementation.
There are several variations on the strategy pattern, the simplest of which is outlined below:

This first code snippet outlines a family of algorithms; you may want a serialized array, some JSON or maybe 
just an array of data:
{% highlight php %}
<?php

interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
{% endhighlight %}

By encapsulating the above algorithms you are making it nice and clear in your code that other developers can easily 
add new output types without affecting the client code.

You will see how each concrete 'output' class implements an OutputInterface - this serves two purposes, primarily it
provides a simple contract which must be obeyed by any new concrete implementations. Secondly by implementing a common
interface you will see in the next section that you can now utilise [Type Hinting](http://php.net/manual/en/language.oop5.typehinting.php) to ensure that the client which is utilising these behaviours is of the correct type in
this case 'OutputInterface'.

The next snippet of code outlines how a calling client class might use one of these algorithms and even better set the
behaviour required at runtime:
{% highlight php %}
<?php

class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}
{% endhighlight %}

The calling client class above has a private property which must be set at runtime and be of type 'OutputInterface'
once this property is set a call to loadOutput() will call the load() method in the concrete class of the output type
that has been set.
{% highlight php %}
<?php

$client = new SomeClient();

// Want an array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Want some JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [Strategy pattern on Wikipedia](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller

Il _Front Controller Pattern_ consiste nell'utilizzo di un singolo punto di entrata per la tua applicazione Web (es.
index.php) che gestisce tutte le richieste. Questo codice è responsabile di caricare di tutte le dipendenze, di
processare la richiesta e di inviare la risposta al browser. Il _Front Controller Pattern_ può portare benefici perché
incoraggia l'uso di codice modulare e fornisce un punto centrale in cui inserire codice che dev'essere eseguito per ogni
richiesta (come la sanificazione dell'input).

* [Front Controller Pattern su Wikipedia](https://it.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller

Il pattern _Model-View-Controller_ (MVC), e i collegati HMVC e MVVM,  permettono di dividere il codice in oggetti logici
che hanno funzioni altamente specifiche. I modelli servono come layer di accesso ai dati, dove i dati vengono recuperati
e restituiti in formati utilizzabili all'interno della tua applicazione. I controller gestiscono la richiesta, processano
le informazioni restituite dai modelli e caricano le viste che inviano in risposta. Le viste sono dei template (markup,
XML ecc.) che vengono inviati in risposta al browser Web.

MVC è il pattern architetturale più comune usato nei [framework PHP](https://github.com/codeguy/php-the-right-way/wiki/Frameworks)
famosi.

Il pattern model-view-controller (MVC) e i suoi parenti HMVC e MVVM ti consentono di dividere il codice in oggetti logici
che eseguono compiti specifici. I modelli sono un livello di accesso ai dati, dove questi sono recuperati e restituiti in
formati utilizzabili nella tua applicazione. I controller gestiscono la richiesta, processano i dati restituiti dai modelli
e caricano le visite da mandare come risposta. Le viste sono template (markup, XML etc.) da visualizzare che vengono inviati
come risposta la browser web.

Impara di più riguardo l'MVC e i pattern a esso collegati:

* [MVC](https://it.wikipedia.org/wiki/Model-View-Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
