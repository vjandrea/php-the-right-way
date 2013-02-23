---
isChild: true
title: Namespace
---

## Namespace {#namespace_title}

Come menzionato sopra, la comunità PHP ha molti sviluppatori che creano molto
codice. Questo significa che il codice PHP di una libreria potrebbe usare lo
stesso nome di un'altra per una classe. Quando entrambe le librerie vengono
usate nello stesso namespace, potrebbero collidere e causare problemi.

I _namespace_ risolvono questo problema. Come descritto nel manuale di PHP, si
può pensare ai namespace come directory del sistema operativo che dividono i
file; due file con lo stesso nome possono esistere in directory separate. Allo
stesso modo, due classi PHP con lo stesso nome possono esistere in namespace PHP
separati. È così semplice.

È importante inserire il codice in un namespace in modo che possa essere usato
da altri sviluppatori senza paura che esso collida con altre librerie.

Un modo consigliato per usare i namespace è descritto nel [PSR-0][psr0], che
si pone come obiettivo quello di creare una convenzione standard per i file, le
classi e i namespace, consentendo così il plug-and-play del codice.

* [Leggi sui namespace][namespaces]
* [Leggi il PSR-0][psr0]

[namespaces]: http://php.net/manual/en/language.namespaces.php
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
