---
isChild: true
title:   Cache del bytecode
---

## Cache del bytecode {#cache_del_bytecode_title}

Quando un file PHP viene eseguito, esso viene prima compilato in bytecode (anche
conosciuto come opcode) e, solo allora, il bytecode viene eseguito. Se un file
PHP non viene modificato, il bytecode rimarrà sempre lo stesso. Questo significa
che questo passo della compilazione è uno spreco di CPU.

A questo punto entra in gioco la cache del bytecode. Essa previene compilazioni
ridondanti salvando il bytecode in memoria e riusandolo per le chiamate
successive. Impostare la cache del bytecode è una questione di minuti, e la tua
applicazione sarà molto più veloce. Non c'è davvero ragione per non volerla
usare.

Alcune cache del bytecode famose sono:

* [APC](http://php.net/manual/en/book.apc.php)
* [XCache](http://xcache.lighttpd.net/)
* [Zend Optimizer+](http://www.zend.com/products/server/) (parte del pacchetto Zend Server)
* [WinCache](http://www.iis.net/download/wincacheforphp) (estensione per MS Windows Server)
