---
layout: page
title: Design Pattern
---

# Design Pattern

Ci sono diversi modi di strutturare il codice e il progetto per la tua
applicazione Web, e puoi sforzarti quanto preferisci nell'architettarli.
Generalmente, però, è una buona idea seguire dei modelli comuni, in modo da
rendere il tuo codice più semplice da gestire per te e più facile da leggere per
gli altri.

* [Modelli architetturali su Wikipedia](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Design pattern su Wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)

## Factory

Uno dei design pattern più usati è il _Factory Method_. In questo pattern, una
classe crea l'oggetto che vuoi utilizzare. Considera il seguente esempio di
_Factory Method_:

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

Questo codice usa una _factory_ per creare l'oggetto Automobile. Ci sono due
potenziali benefici nello strutturare il codice in questo modo. Il primo è che,
se in futuro avrai bisogno di rinominare, modificare o sostituire la classe
Automobile, dovrai solamente modificare la _factory_ invece di ogni riga del tuo
codice che usa la classe Automobile. Il secondo beneficio è che, se creare un
oggetto è un lavoro complicato, puoi fare tutto nella _factory_ invece di
ripeterlo ogni volta che vuoi creare una nuova istanza.

Usare il _Factory Method_ non è sempre necessario (né saggio). Il codice di
esempio mostrato qui è così semplice che aggiungere una _factory_ significa solo
complicare inutilmente l'applicazione. Tuttavia, se stai creando un progetto
grande o complesso, potresti volerti risparmiare molta fatica usando le
_factory_.


* [Factory Method su Wikipedia](https://it.wikipedia.org/wiki/Factory_method)

## Singleton

Durante la progettazione di un'applicazione Web, è spesso sensato
concettualmente e architetturalmente permettere l'accesso a una e una sola
istanza di una specifica classe. Il pattern _singleton_ ci permette di fare ciò.

{% highlight php %}
<?php
class Singleton
{
    static $instance;

    private function __construct()
    {
    }

    public static function getInstance()
    {
        if (!isset(self::$instance)) {
            self::$instance = new self();
        }

        return self::$instance;
    }
}

$instance1 = Singleton::getInstance();
$instance2 = Singleton::getInstance();

echo $instance1 === $instance2; // visualizza 1
{% endhighlight %}

Il codice qui sopra implementa il _singleton_ utilizzando una variabile statica
e il metodo `getInstance()`. Nota come il costruttore viene dichiarato privato
per prevenire l'istanziamento della classe tramite la keyword `new`.

Il pattern _Singleton_ è utile quando dobbiamo assicurarci che esiste una sola
istanza di una classe per l'intero ciclo di vita della richiesta in
un'applicazione Web. Ci troviamo spesso in questa situazione quando abbiamo
degli oggetti globali (come una classe Configuration) o una risorsa condivisa
(come una coda di eventi).

Dovresti stare molto attento quando usi il pattern _Singleton_, perché per
definizione introduce uno stato globale nella tua applicazione, riducendo la
testabilità. Nella maggior parte dei casi, l'iniezione delle dipendenze può
(e dovrebbe) essere usata al posto di una classe _Singleton_. Utilizzando
l'iniezione delle dipendenze non dobbiamo introdurre alcun legame nel design
della nostra applicazione, perché l'oggetto che utilizza una risorsa globale o
condivisa non dev'essere a conoscenza di alcuna classe concretamente definita.

* [Singleton su Wikipedia](https://it.wikipedia.org/wiki/Singleton)

## Front Controller

Il _Front Controller Pattern_ consiste nell'utilizzo di un singolo punto di
entrata per la tua applicazione Web (es. index.php) che gestisce tutte le
richieste. Questo codice è responsabile di caricare di tutte le dipendenze, di
processare la richiesta e di inviare la risposta al browser. Il _Front
Controller Pattern_ può portare benefici perché incoraggia l'uso di codice
modulare e fornisce un punto centrale in cui inserire codice che dev'essere
eseguito per ogni richiesta (come la sanificazione dell'input).

* [Front Controller Pattern su Wikipedia](https://it.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller

Il pattern _Model-View-Controller_ (MVC), e i collegati HMVC e MVVM,  permettono
di dividere il codice in oggetti logici che hanno funzioni altamente specifiche.
I modelli servono come layer di accesso ai dati, dove i dati vengono recuperati
e restituiti in formati utilizzabili all'interno della tua applicazione. I
controller gestiscono la richiesta, processano le informazioni restituite dai
modelli e caricano le viste che inviano in risposta. Le viste sono dei template
(markup, XML ecc.) che vengono inviati in risposta al browser Web.

MVC è il pattern architetturale più comune usato nei
[framework PHP](https://github.com/codeguy/php-the-right-way/wiki/Frameworks)
famosi.

The model-view-controller (MVC) pattern and its relatives HMVC and MVVM let you break up code into logical objects that
serve very specific purposes. Models serve as a data access layer where data is fetched and returned in formats usable
throughout your application. Controllers handle the request, process the data returned from models and load views to
send in the response. And views are display templates (markup, xml, etc) that are sent in the response to the web
browser.

Impara di più riguardo l'MVC e i pattern a esso collegati:

* [MVC](https://it.wikipedia.org/wiki/Model-View-Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
