---
isChild: true
anchor:  opcode_cache
---

## Opcode cache {#opcode_cache_title}

Quando un nuovo PHP file viene eseguito, è prima compilato in opcode; solo dopo
l'opcode viene eseguito. Se un file PHP non viene modificato, l'opcode rimane lo
stesso. Questo significa che il processo di compilazione è uno spreco di risorse
computazionali.

È qui che le cache dell'opcode entrano in gioco. Evitano compilazioni inutili
salvando l'opcode in memoria e riusandolo nelle chiamate successive. Impostare
una cache dell'opcode è una questione di minuti, e la tua applicazione sarà
molto più veloce. Non c'è alcuna ragione per non usarla.

A partire da PHP 5.5, c'è una cache dell'opcode integrata chiamata
[OPcache][opcache-book]. È anche disponibile per versioni precedenti.

Altre risorse sulle cache dell'opcode:

* [OPcache][opcache-book] (integrata a partire da PHP 5.5)
* [APC] (PHP 5.4 e precedenti)
* [XCache]
* [Zend Optimizer+] (parte del pacchetto Zend Server)
* [WinCache] (estensione per MS Windows Server)
* [lista di acceleratori PHP su Wikipedia][PHP_accelerators]

[opcache-book]: http://php.net/book.opcache
[APC]: http://php.net/book.apc
[XCache]: http://xcache.lighttpd.net/
[Zend Optimizer+]: http://www.zend.com/products/server/
[WinCache]: http://www.iis.net/download/wincacheforphp
[PHP_accelerators]: http://en.wikipedia.org/wiki/List_of_PHP_accelerators
