---
isChild: true
title:   Server virtuali o dedicati
anchor:  virtual_or_dedicated_servers
---

## Server virtuali o dedicati {#virtual_or_dedicated_servers_title}

Se hai dimestichezza con l'amministrazione di un sistema o vuoi impararla, i
server virtuali o dedicati ti danno totale controllo sull'ambiente di produzione
della tua applicazione.

### nginx e PHP-FPM

PHP, tramite il FastCGI Process Manager (FPM) integrato, si integra molto bene
con [nginx], che è un server leggero dalle alte prestazioni. Usa meno memoria di
Apache e gestisce meglio le richieste simultanee. Questo è particolarmente
importante su server virtuali che non hanno molta memoria.

* [Scopri nginx][nginx]
* [Scopri PHP-FPM][phpfpm]
* [Scopri come configurare nginx e PHP-FPM in modo sicuro][secure-nginx-phpfpm]

### Apache e PHP

PHP e Apache hanno fatto molta storia insieme. Apache è totalmente configurabile
e ha molti [moduli][apache-modules] che estendono le sue funzionalità. È una
scelta comune per i server condivisi e una configurazione facile per i framework
PHP e le applicazioni open source come WordPress. Sfortunatamente, Apache usa
più risorse di nginx di default e non riesce a gestire così tanti visitatori
contemporeanei.

Ci sono molte configurazioni diverse per eseguire Apache con PHP. La più comune
e la più semplice da configurare è il [prefork MPM] con mod_php5. Nonostante
questa non sia la più efficiente in termini di consumo di memoria, è la più
semplice da configurare e usare. Questa è probabilmente la scelta migliore se
non vuoi addentrarti troppo in profondità nell'amministrazione dei server. Nota
che per usare mod_php5 DEVI usare il prefork MPM.

In alternativa, se vuoi ottenere migliori performance e stabilità con Apache
puoi usare lo stesso sistema FPM di nginx ed eseguire l'[MPM worker] o
l'[MPM event] con mod_fastcgi o mod_fcgid. Questa configurazione sarà molto più
efficiente nell'utilizzo di memoria e molto più veloce, ma è più complicata da
installare.

* [Scopri Apache][apache]
* [Scopri i Multi-Processing Modules][apache-MPM]
* [Scopri mod_fastcgi][mod_fastcgi]
* [Scopri on mod_fcgid][mod_fcgid]

[nginx]: http://nginx.org/
[phpfpm]: http://php.net/install.fpm
[secure-nginx-phpfpm]: https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/
[apache-modules]: http://httpd.apache.org/docs/2.4/mod/
[prefork MPM]: http://httpd.apache.org/docs/2.4/mod/prefork.html
[worker MPM]: http://httpd.apache.org/docs/2.4/mod/worker.html
[event MPM]: http://httpd.apache.org/docs/2.4/mod/event.html
[apache]: http://httpd.apache.org/
[apache-MPM]: http://httpd.apache.org/docs/2.4/mod/mpm_common.html
[mod_fastcgi]: http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html
[mod_fcgid]: http://httpd.apache.org/mod_fcgid/
