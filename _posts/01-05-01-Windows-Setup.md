---
isChild: true
title: Configurazione Windows
---

## Configurazione Windows {#configurazione_windows_title}

PHP è disponibile in diversi modi per Windows. Puoi
[scaricare i binari][php-downloads] e, fino a poco tempo fa, potevi usare un
installer '.msi'. L'installer non è più disponibile e si ferma a PHP 5.3.0.

Per l'apprendimento e lo sviluppo locale puoi usare il server integrato di PHP
5.4, quindi non dovrai preoccuparti di configurarlo.

Se preferisci un pacchetto "all-in-one" che comprende un Web server completo e
MySQL, strumenti come il [Web Platform Installer][wpi], [Zend Server CE][zsce],
[XAMPP][xampp] e [WAMP][wamp] ti aiuteranno a configurare il tuo ambiente
Windows in men che non si dica. Detto ciò, questi strumenti saranno leggermente
diversi dall'ambiente di produzione, quindi fai attenzione alle differenze se
stai lavorando su Windows e distribuendo su Linux.

Se devi eseguire un ambiente di produzione su Windows, IIS7 ti fornirà un
ambiente stabile e performante. Puoi usare [phpmanager][phpmanager] (un plugin
della GUI per IIS7) per rendere la configurazione e la gestione di PHP semplice.
IIS7 integra FastCGI, devi solo configurare PHP come handler. Per supporto e
ulteriori risorse, c'è un'[area dedicata a PHP su iis.net][php-iis].

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[zsce]: http://www.zend.com/it/products/server-ce/
[xampp]: http://www.apachefriends.org/it/xampp.html
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/
