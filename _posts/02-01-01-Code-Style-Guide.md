---
title:  Stile di codifica
anchor: code_style_guide
---

# Stile di codifica {#code_style_guide_title}

La comunità PHP è grande e diversificata, fatta di innumerevoli librerie,
framework e componenti. È comune per gli sviluppatori PHP scegliere diversi di
questi e combinarli in un singolo progetto. È importante che il codice PHP
aderisca (il più fedelmente possibile) a uno stile di codifica comune per
rendere facile agli sviluppatori mischiare e usare diverse librerie nei loro
progetti.

Il [Framework Interop Group][fig] ha proposto e approvato una serie di
raccomandazioni di stile. Non tutte riguardano lo stile del codice, ma quelle
che lo riguardano sono note come [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] e
[PSR-4][psr4]. Queste raccomandazioni non sono che una lista di regole che
alcuni progetti come Drupal, Zend, Symfony, CakePHP, phpBB, AWS SDK, FuelPHP,
Lithium etc. stanno iniziando ad adottare. Puoi usarle in uno dei tuoi progetti,
o continuare a usare il tuo stile personale.

Idealmente dovresti scrivere codice PHP che aderisce ad uno standard noto. Può
essere una qualunque combinazione dei PSR o uno degli standard di codifica di
PHP o Zend. Questo significa che altri sviluppatori potranno facilmente leggere
e lavorare col tuo codice, e le applicazioni che implementano i componenti
potranno essere consistenti anche quando lavorano con molto codice di terze
parti.

* [Leggi il PSR-0][psr0]
* [Leggi il PSR-1][psr1]
* [Leggi il PSR-2][psr2]
* [Leggi il PSR-4][psr4]
* [Leggi i PEAR Coding Standards][pear-cs]
* [Leggi i Symfony Coding Standards][symfony-cs]

Puoi usare [PHP_CodeSniffer][phpcs] per controllare che il codice rispetti
queste raccomandazioni, e plugin per editor di testo come
[Sublime Text 2][st-cs] per avere feedback in tempo reale.

Puoi sistemare la disposizione del codice automaticamente usando uno dei due
strumenti disponibili. Uno è il [PHP Coding Standards Fixer][phpcsfixer] di
Fabien Potencier, testato scrupolosamente. È più grande e più lento, ma molto
stabile e usato da alcuni grandi progetti come Magento e Symfony. Un'altra
opzione è [php.tools][phptools], reso popolare dal plugin per editor
[sublime-phpfmt][sublime-phpmft]. Nonostante sia nuovo, porta molti
miglioramenti sotto il punto di vista della performance, quindi l'adattamento in
tempo reale nell'editor è più fluido.

La lingua inglese è preferita per tutti i nomi di simboli e infrastrutture del
codice. I commenti possono essere scritti in qualunque lingua facilmente
comprensibile da tutte le parti presenti e future che dovranno lavorare sul
codice.

[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
[phptools]: https://github.com/dericofilho/php.tools
[sublime-phpfmt]: https://github.com/dericofilho/sublime-phpfmt
