---
layout: page
title: Le basi
---

# Le basi

## Operatori di confronto

Gli operatori di confronto sono spesso un aspetto trascurato di PHP, il che può
portare a molti risultati inaspettati. Uno di questi problemi deriva dai
conforonti stretti (i confronti di valori booleani come se fossero interi).

{% highlight php %}
<?php
$a = 5;   // 5 come intero

var_dump($a == 5);       // confronta il valore; restituisce vero
var_dump($a == '5');     // confronta il valore (ignora il tipo); restituisce vero
var_dump($a === 5);      // confronta tipo/valore (intero e intero); restituisce vero
var_dump($a === '5');    // confronta tipo/valore (intero e intero); restituisce falso

/**
 * Confronti stretti
 */
if (strpos('testing', 'test')) {    // 'test' è trovato alla posizione 0, che è interpretato come il booleano falso
    // codice...
}

// contro

if (strpos('testing', 'test') !== false) {    // vero, perché è stato fatto un confronto stretto (0 !== false)
    // codice...
}
{% endhighlight %}

* [Operatori di confronto](http://php.net/manual/it/language.operators.comparison.php)
* [Tabella di confronto tra tipi](http://php.net/manual/it/types.comparisons.php)

## Istruzioni condizionali

### Istruzioni if

Nell'utilizzo di istruzioni 'if/else' in una funzione o in una classe, si pensa
spesso che 'else' debba essere necessariamente usato per potenziali risultati.
Ma se il risultato è la restituzione di un valore, 'else' non è necessario,
perché 'return' terminerà la funzione, rendendo 'else' inutile.

{% highlight php %}
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

// contro

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else non è necessario
}
{% endhighlight %}

* [Costrutti if](http://php.net/manual/it/control-structures.if.php)

### Istruzioni switch

Le istruzioni switch sono un ottimo modo per evitare di scrivere infiniti if ed
elseif, ma ci sono un paio di cose a cui prestare attenzione:

- Le istruzioni switch confrontano solo i valori, non il tipo (equivalente a
'==')
- Iterano caso dopo caso finché non viene trovata una corrispondenza. Se non
viene trovata, viene eseguita quella di default (se definita)
- Senza un 'break', continueranno a implementare ogni caso finché non raggiungono
un break/return
- In una funzione, l'utilizzo di 'return' elimina la necessità per un 'break',
perché esso termina la funzione

{% highlight php %}
<?php
$answer = test(2);    // sia il codice del 'case 2', sia quello del 'case 3' saranno implementati

function test($a)
{
    switch ($a) {
        case 1:
            // codice...
            break;             // break viene usato per terminare l'istruzione switch
        case 2:
            // codice...         // senza un break, il confronto continua fino al caso 3
        case 3:
            // codice...
            return $result;    // in una funzione, 'return' termina la funzione
        default:
            // codice...
            return $error;
    }
}
{% endhighlight %}

* [Istruzioni switch](http://php.net/manual/it/control-structures.switch.php)
* [PHP switch](http://phpswitch.com/)

## Namespace globale

Quando usi i namespace, potresti scoprire che le funzioni native sono nascoste
dalle funzioni che hai scritto. Per sistemarlo, referenzia la funzione globale
mettendo un backslash prima del nome della funzione.

{% highlight php %}
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // Il nome della nostra funzione è lo stesso di una nativa.
                         // Esegui la funzione native aggiungendo '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator è una classe nativa. Usare il suo nome senza un backslash
                                         // significa cercare di risolverla nel tuo namespace.
}
{% endhighlight %}

* [Spazio globale](http://php.net/manual/it/language.namespaces.global.php)
* [Regole globali](http://php.net/manual/it/userlandnaming.rules.php)

## Stringhe

### Concatenamento

- If your line extends beyond the recommended line length (120 characters), consider concatenating your line
- For readability it is best to use concatenation operators over concatenating assignment operators
- While within the original scope of the variable, indent when concatenation uses a new line

- Se la tua linea eccede la lunghezza raccomandata (120 caratteri), considera il concatenamento
- Per leggibilità è meglio usare gli operatori di concatenamento invece che gli operatori concatenanti di assegnazione
- Se ti trovi nello scope originale della variabile, usa l'indentazione quando il concatenamento occupa una nuova linea

{% highlight php %}
<?php
$a  = 'Esempio multi-linea';    // operatore di assegnazione/concatenamento (.=)
$a .= "\n";
$a .= 'di cosa non fare';

// vs

$a = 'Esempio multi-linea'      // operatore di concatenamento (.)
    . "\n"                     // indentazione delle nuove linee
    . 'di cosa fare';
{% endhighlight %}

* [Operatori delle stringhe](http://php.net/manual/it/language.operators.string.php)

### Tipi di stringhe

I tipi di stringhe sono una funzionalità costante nella comunità PHP, ma questa
sezione spiegherà comunque le differenze tra i tipi di stringhe e i loro
usi/benefici.

#### Apici singoli

Gli apici singoli sono il modo più semplice di definire una stringa e sono
spesso il più veloce. La loro velocità deriva dal fatto che PHP non ha bisogno
di interpretare la stringa (non cerca variabili). Sono adatte per:

- Stringhe che non devono essere interpretate
- Scrittura di una variabile sotto forma di testo semplice

{% highlight php %}
<?php
echo 'Questa è la mia stringa, guarda come è bella.';    // non serve interpretare una stringa semplice

/**
 * Output:
 *
 * Questa è la mia stringa, guarda come è bella.
 */
{% endhighlight %}

* [Apici singoli](http://www.php.net/manual/it/language.types.string.php#language.types.string.syntax.single)

#### Virgolette

Le virgolette sono il coltellno svizzero delle stringhe, ma sono più lente
perché vengono interpretate. Sono adatte per:

- Stringhe con caratteri di escape
- Stringhe con variabili e testo semplice
- Condensare il concatenamento multi-riga e migliorare la leggibilità

{% highlight php %}
<?php
echo 'phptherightway è ' . $adjective . '.'     // un esempio con apici singoli che usa concatenamento multiplo per
    . "\n"                                      // variabili e caratteri di escape
    . 'Adoro imparare' . $code . '!';

// contro

echo "phptherightway è $adjective.\n Adoro imparare $code!"    // Invece del concatenamento multiplo, le virgolette
                                                               // ci permettono di creare una stringa interpretata
{% endhighlight %}

Nell'uso di stringhe contenenti variabili e racchiuse tra virgolette doppie, capita
spesso che il nome della variabile tocchi un altro carattere. In questo caso PHP
non interpreterà la variabile perché il suo nome è nascosto. Per ovviare a
questo problema, racchiudi la variabili tra parentesi graffe.

{% highlight php %}
<?php
$juice = 'prugn';
echo "Ho bevuto del succo fatto con le $juicee";    // $juice non può essere interpetato

// contro

$juice = 'prugn';
echo "Ho bevuto del succo fatto con le {$juice}e";    // $juice verrà interpretato

/**
 * Anche le variabili complesse possono essere racchiuse tra parentesi graffe
 */

$juice = array('mel', 'banan', 'prugn');
echo "Ho bevuto del succo fatto con le {$juice[1]}e";   // $juice[1] verrà interpretato
{% endhighlight %}

* [Virgolette](http://www.php.net/manual/it/language.types.string.php#language.types.string.syntax.double)

#### Sintassi nowdoc

La sintassi nowdoc è stata introdotta in PHP 5.3 e internamente funziona nello
stesso modo degli apici singoli, ma è adatta per creare stringhe multi-linea
senza dover usare il concatenamento.

{% highlight php %}
<?php
$str = <<<'EOD'             // inizializzata da <<<
Esempio di stringa
che occupa più linee
utilizzando la sintassi nowdoc.
$a non viene interpretato.
EOD;                        // la chiusura di 'EOD' dev'essere su una linea a parte, e senza indentazione

/**
 * Output:
 *
 * Esempio di stringa
 * che occupa più linee
 * utilizzando la sintassi Nowdoc.
 * $a non viene interpretato.
 */
{% endhighlight %}

* [Sintassi nowdoc](http://www.php.net/manual/it/language.types.string.php#language.types.string.syntax.nowdoc)

#### Sintassi heredoc

La sintassi heredoc internamente funziona nello stesso modo delle virgolette, ma
è adatta per la creazione di stringhe multi-linea senza la necessità di
concatenamento.

{% highlight php %}
<?php
$a = 'variabili';

$str = <<<EOD               // inizializzata da <<<
Esempio di stringa
che occupa più linee
utilizzando la sintassi heredoc.
Le $a sono interpretate.
EOD;                        // la chiusura di 'EOD' dev'essere su una linea a parte, e senza indentazione

/**
 * Output:
 *
 * Esempio di stringa
 * che occupa più linee
 * utilizzando la sintassi heredoc.
 * Le variabili sono interpretate.
 */
{% endhighlight %}

* [Sintassi heredoc](http://www.php.net/manual/it/language.types.string.php#language.types.string.syntax.heredoc)

## Operatore ternario

L'operatore ternario è un ottimo modo per sintetizzare il codice, ma viene
spesso abusato. Anche se gli operatori ternari possono essere nidificati, è
consigliato usarne uno per riga per leggibilità.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? 'sì' : 'no';
{% endhighlight %}

Ecco invece un esempio che sacrifica ogni forma di leggibilità per ridurre il numero delle righe:

{% highlight php %}
<?php
echo ($a) ? ($a == 5) ? 'sì' : 'no' : ($b == 10) ? 'troppo' : ':(';    // eccessiva nidificazione, sacrifica la leggibilità
{% endhighlight %}

Per restituire un valore con gli operatori ternari usa la sintassi corretta.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // questo esempio mostrerà un errore

// contro

$a = 5;
return ($a == 5) ? 'sì' : 'no';    // questo esempio restituirà 'sì'

{% endhighlight %}

È importante notare che non serve usare l'operatore ternario per restituire un valore booleano. Un esempio:

{% highlight php %}
<?php
$a = 3;
return ($a == 3) ? true : false; // Restituirà true o false a seconda della condizione $a == 3

// vs

$a = 3;
return $a == 3; // Restituirà true o false a seconda della condizione $a == 3

{% endhighlight %}

Lo stesso si può dire per tutte le operazioni (===, !==, !=, == etc.)

#### Uso delle parentesi con gli operatori ternari per forma e funzione

Quando usi l'operatore ternario, le parentesi possono fare la loro parte per migliorare la leggibilità e anche per unire più condizioni in blocchi di istruzioni. Un esempio di un uso superfluo delle parentesi è:

{% highlight php %}
<?php
$a = 3;
return ($a == 3) ? "sì" : "no"; // restituisce sì o no a seconda della condizione $a == 3

// contro

<?php
$a = 3;
return $a == 3 ? "sì" : "no"; // restituisce sì o no a seconda della condizione $a == 3
{% endhighlight %}

Le parentesi permettono anche di creare unioni in un blocco di istruzioni, in
modo che il blocco venga controllato come una sola condizione. Ecco un esempio
in cui il blocco restituirà true se sia ($a == 3 e $b == 4) che $c == 5 sono
veri.

{% highlight php %}
<?php
return ($a == 3 && $b == 4) && $c == 5;
{% endhighlight %}

Un altro esempio è la porzione qui sotto che restituirà true se ($a != 3 E $b !=
4) O $C == 5.

{% highlight php %}
<?php
return ($a != 3 && $b != 4) || $c == 5;
{% endhighlight %}

* [Operatore ternario](http://php.net/manual/it/language.operators.comparison.php)

## Dichiarazioni di variabili

A volte, gli sviluppatori cercano di rendere il loro codice "più pulito"
dichiarando variabili predefinite con un nome differente.  Ciò che questo
comporta, in realtà, è un raddoppiamento del consumo di memoria dello script.
Nell'esempio sottostante, presumiamo che una stringa di esempio contenga dati
per 1MB. Copiando la variabile hai portato il consumo di memoria dello script a
2MB.

{% highlight php %}
<?php
$about = 'Una stringa molto lunga';    // usa 2MB di memoria
echo $about;

// contro

echo 'Una stringa molto lunga';        // usa 1MB di memoria
{% endhighlight %}

* [Consigli di performance](https://developers.google.com/speed/articles/optimizing-php)
