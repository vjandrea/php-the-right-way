---
isChild: true
---

## Vagrant {#vagrant_title}

Eseguire la tua applicazione in ambienti differenti in sviluppo e produzione può portare a strani bug che compaiono solo
quando il sito è pubblicato. Inoltre è difficile fare in modo che la stessa versione di ogni libreria sia usata quando
si fa parte di un team di sviluppatori.

Se stai sviluppando su Windows e pubblicando su Linux (o qualunque cosa non sia Windows) o stai sviluppando in un team,
potresti considerare l'utilizzo di una macchina virtuale. Sembra complicato, ma tramite [Vagrant][vagrant] puoi
configurare una semplice macchina virtuale in pochi passi. Queste macchine di base possono essere configurate
manualmente, ma puoi usare un software di gestione come [Puppet][puppet] o [Chef][chef] per farlo al posto tuo. Questo è
un buon modo per assicurarsi che diverse macchine vengano configurate nella stessa identica maniera e rimuove la
necessità per complicate liste di comandi di configurazione. Puoi anche "distruggere" la macchina e ricrearla senza
troppa fatica, rendendo facile la creazione di un'installazione "fresca".

Vagrant crea cartelle condivise usate per condividere il codice tra l'host e la tua macchina virtuale, dunque puoi
creare e modificare i file sulla macchina host ed eseguirlo nella macchina virtuale.

### Un piccolo aiuto

Se ti serve un piccolo aiuto per iniziare a usare Vagrant eccoti due servizi che potrebbero essere utili:

- [Rove][rove]: servizio che ti permette di pregenerare build di Vagrant tipiche, tra cui PHP. Il provisioning è
  eseguito con Chef.
- [Puphpet][puphpet]: una semplice GUI per configurare macchine virtuali per lo sviluppo PHP. **Fortemente orientato
  verso PHP**. Oltre alle VM locali, può essere usato per pubblicare anche servizi cloud. Il provisioning è eseguito
  con Puppet.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
