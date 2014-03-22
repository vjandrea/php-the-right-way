---
title: Gestione delle dipendenze
anchor: dependency_management
---

# Gestione delle dipendenze {#gestione_delle_dipendenze_title}

Ci sono moltissime librerie PHP, framework e componenti tra cui scegliere. Il
tuo progetto, probabilmente, ne userà diversi. Queste sono dipendenze del
progetto. Fino a poco tempo fa, PHP non aveva un buon modo per gestire le
dipendenze del progetto. Anche se le gestivi manualmente, dovevi comunque
preoccuparti degli autoloader. Non più.

Attualmente ci sono due grandi sistemi di gestione dei pacchetti per PHP:
Composer e PEAR. Qual è meglio per te? La risposta è entrambi.

 * Usa **Composer** quando gestisci le dipendenze di un singolo progetto.
 * Usa **PEAR** quando gestisci le dipendenze di PHP per l'intero sistema.

In genere, i pacchetti di Composer saranno disponibili solo nei progetti che
specifichi esplicitamente, mentre i pacchetti di PEAR saranno disponibili per
tutti i tuoi progetti PHP. Anche se PEAR può sembrare l'approccio più semplice
a prima vista, ci sono vantaggi nell'utilizzo di un approccio
progetto-per-progetto per le tue dipendenze.
