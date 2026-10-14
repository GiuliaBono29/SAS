# SAS – Analisi e Progettazione di un sistema per la gestione di eventi di catering

## Introduzione

Progetto del corso di **Strumenti e Metodi per l'Analisi del Software** (Laurea Triennale in Informatica, UniTo).
Il progetto riguarda l'**analisi e la progettazione orientata agli oggetti** di un sistema per la gestione di un servizio di catering. Sono stati sviluppati due casi d'uso, con attori e momenti diversi:

* **Gestione Foglio Riepilogativo**: cosa si cucina (attore: Chef)
* **Gestione Turni**: quando e dove si lavora (attore: Organizzatore)

I due casi d'uso si collegano tramite il **turno**: l'Organizzatore crea e pubblica i turni, lo Chef assegna a quei turni i compiti del suo foglio.

Non è prevista un'implementazione: il progetto consiste nella documentazione di analisi e progettazione. Il progetto è stato sviluppato in gruppo per il corso di SAS, insieme a un collaboratore.

## Tecnologie usate

* UML, con **UMLet** per i diagrammi (file `.uxf`)
* Metodologia in stile **Larman**: casi d'uso, diagrammi di sequenza di sistema, contratti delle operazioni, glossario, diagrammi di sequenza di progetto
* Pattern: **Controller** (`SheetManager`, `CalendarManager`, `UserManager`) e **Observer** (`SheetEventReceiver`, `CalendarEventReceiver`)

## Riassunto delle parti

### Parte 1 – Gestione Foglio Riepilogativo

Lo Chef crea un foglio riepilogativo del servizio, aggiunge i compiti, li ordina e li assegna a un turno di cucina ed eventualmente a un cuoco. Può anche modificare o eliminare compiti, assegnazioni e il foglio stesso.



Passaggi di progettazione:

* Caso d'uso: scenario principale (crea foglio, aggiungi compito, ordina, assegna a turno/cuoco, modifica valori) ed estensioni/eccezioni (eliminazione di foglio, compito o assegnazione; cuoco non assegnabile).
* Glossario: definizione dei termini del dominio (Chef, Cuoco, Organizzatore, Personale, ecc.).
* Diagrammi di sequenza di sistema (SSD): scenario base, estensioni ed eccezioni, con frame alt/opt/loop.
* Contratti delle operazioni: pre-condizioni e post-condizioni di ogni operazione (es. creaFoglioRiepilogativo, aggiungeCompito, assegnaCompito).
* Diagrammi di sequenza di progetto (DSD): assegnazione delle responsabilità alle classi (SheetManager, UserManager, SummarySheet, Task, CookingTurn), controllo dei ruoli (solo lo Chef può operare), gestione delle eccezioni e notifica delle modifiche con il pattern Observer.



### Parte 2 – Gestione Turni

L'Organizzatore apre o crea il proprio calendario e crea i turni di cucina (anche ricorrenti, affittati o straordinari) e di servizio. Può raggrupparli in blocchi, modificarli o eliminarli, e infine pubblicare il calendario, così che i cuochi vengano notificati.



Passaggi di progettazione:

* Analisi delle attività: descrizione del lavoro dei due utenti tipo (la wedding planner e il titolare del catering) e sintesi in un processo combinato, da cui è nato il caso d'uso.
* Caso d'uso: scenario principale (scelta del calendario, creazione dei turni, raggruppamento in blocchi, pubblicazione) ed estensioni/eccezioni (creazione e reset del calendario, turno già presente nella stessa data, ora e luogo, eliminazione oltre la data limite).
* Diagrammi di sequenza di sistema (SSD): scenario base ed estensioni ed eccezioni.
* Contratti delle operazioni: ad esempio CreaTurnoCucina (anche ricorrente), RaggruppaTurni, Pubblica.
* Diagrammi di sequenza di progetto (DSD): uno per operazione (apertura e creazione calendario, creazione dei turni, eliminazione, modifica, blocchi, pubblicazione). Le responsabilità sono assegnate a CalendarManager, Calendar, Turn (CookingTurn, ServiceTurn), Block e PlaceDate; la pubblicazione notifica i cuochi con il pattern Observer (CalendarEventReceiver).

