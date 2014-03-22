---
isChild: true
title:   Cache del bytecode
anchor:  bytecode_cache
---

## Cache del bytecode {#cache_del_bytecode_title}

Quando un file PHP viene eseguito, esso viene prima compilato in bytecode (anche conosciuto come opcode) e, solo allora,
il bytecode viene eseguito. Se un file PHP non viene modificato, il bytecode rimarrà sempre lo stesso. Questo significa
che questo passo della compilazione è uno spreco di CPU.

A questo punto entra in gioco la cache del bytecode. Essa previene compilazioni ridondanti salvando il bytecode in
memoria e riusandolo per le chiamate successive. Impostare la cache del bytecode è una questione di minuti, e la tua
applicazione sarà molto più veloce. Non c'è davvero ragione per non volerla usare.

A partire da PHP 5.5, c'è una cache del bytecode integrata chiamata [OPcache](http://php.net/manual/it/book.opcache.php).
È disponibile anche per versioni precedenti.

Altre cache del bytecode famose sono:

* [APC](http://php.net/manual/en/book.apc.php) (PHP 5.4 and earlier)
* [XCache](http://xcache.lighttpd.net/)
* [Zend Optimizer+](http://www.zend.com/products/server/) (parte del pacchetto Zend Server)
* [WinCache](http://www.iis.net/download/wincacheforphp) (estensione per MS Windows Server)
