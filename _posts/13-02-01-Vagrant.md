---
isChild: true
anchor:  vagrant
---

## Vagrant {#vagrant_title}

[Vagrant][vagrant] ti aiuta a costruire le tue macchine virtuali sfruttando
ambienti virtuali noti, e configura questi ambienti basandosi su un singolo file
di configurazione. Queste macchine possono essere configurate manualmente,
oppure puoi usare un software di "provisioning" come [Puppet][puppet] o
[Chef][chef] per farlo al posto tuo. Eseguire il provisioning della macchina di
base è un ottimo modo per assicurarti che più macchine vengano configurate nella
stessa maniera e rimuove la necessità di mantenere complicate liste di comandi
d'installazione.

Vagrant crea delle cartelle per condividere il codice tra l'host e la tua
macchina virtuale, il che significa che puoi creare e modificare file sul tuo
host e poi eseguire il codice nella macchina virtuale.

### Un po' di aiuto

Se ti serve un picolo aiuto per iniziare a usare Vagrant ci sono dei servizi che
potrebbero essere utili:

- [Rove][rove]: un servizio che ti permette di pre-generare delle build Vagrant
  tipiche (PHP tra le varie opzioni). Il provisioning è effettuato con Chef.

- [Puphpet][puphpet]: una semplice GUI per configurare macchine virtuali per lo
  sviluppo PHP. **Fortemente concentrato su PHP**. Oltre alle macchine virtuali
  locali, può anche essere usato per configurare servizi cloud. Il provisioning
  è effettuato con Puppet.

- [Protobox][protobox]: è un livello costruito su Vagrant con una GUI web per
  configurare macchine virtuali per lo sviluppo web. Un singolo documento YAML
  controlla tutto ciò che viene installato sulla macchina virtuale.

- [Phansible][phansible]: fornisce un'interfaccia di semplice utilizzo che aiuta
  a generare Playbook Ansible per progetti basati su PHP.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
[phansible]: http://phansible.com/
