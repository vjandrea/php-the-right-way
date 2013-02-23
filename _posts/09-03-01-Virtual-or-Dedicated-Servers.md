---
isChild: true
title:   Server virtuali o dedicati
---

## Server virtuali o dedicati {#server_virtuali_o_dedicati_title}

Se hai dimestichezza con l'amministrazione di un sistema o vuoi impararla, i
server virtuali o dedicati ti danno totale controllo sull'ambiente di
produzione della tua applicazione.

### nginx e PHP-FPM

PHP, tramite il FastCGI Process Manager (FPM) integrato, si integra molto bene
con [nginx](http://nginx.org), che è un server leggero dalle alte prestazioni.
Usa meno memoria di Apache e gestisce meglio le richieste simultanee. Questo è
particolarmente importante su server virtuali che non hanno molta memoria.

* [Scopri nginx](http://nginx.org)
* [Scopri PHP-FPM](http://php.net/manual/en/install.fpm.php)
* [Scopri come configurare in sicurezza nginx e PHP-FPM](https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/)

### Apache e PHP

PHP e Apache hanno fatto molta storia insieme. Apache è totalmente configurabile
e ha molti [moduli](http://httpd.apache.org/docs/2.4/mod/) che estendono le sue
funzionalità. È una scelta comune per i server condivisi e una configurazione
facile per i framework PHP e le applicazioni open source come WordPress.
Sfortunatamente, Apache usa più risorse di nginx di default e non riesce a
gestire così tanti visitatori contemporeanei.

Ci sono molte configurazioni diverse per eseguire Apache con PHP. La più comune
e la più semplice da configurare è l'[MPM prefork](http://httpd.apache.org/docs/2.4/mod/prefork.html)
con mod_php5. Nonostante questa non sia la più efficiente in termini di consumo
di memoria, è la più semplice da configurare e usare. Questa è probabilmente la
scelta migliore se non vuoi addentrarti troppo in profondità
nell'amministrazione dei server. Nota che per usare mod_php5 DEVI usare l'MPM
prefork.

In alternativa, se vuoi ottenere migliori performance e stabilità con Apache
puoi usare lo stesso sistema FPM di nginx ed eseguire
l'[MPM worker](http://httpd.apache.org/docs/2.4/mod/worker.html) o
l'[MPM event](http://httpd.apache.org/docs/2.4/mod/event.html) con mod_fastcgi
o mod_fcgid. Questa configurazione sarà molto più efficiente nell'utilizzo di
memoria e molto più veloce, ma è più complicata da installare.

* [Scopri Apache](http://httpd.apache.org/)
* [Scopri i Multi-Processing Modules](http://httpd.apache.org/docs/2.4/mod/mpm_common.html)
* [Scopri mod_fastcgi](http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html)
* [Scopri on mod_fcgid](http://httpd.apache.org/mod_fcgid/)
