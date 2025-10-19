# Shellz

## Descrizione Generale

Shellz è un sistema avanzato per la gestione e il controllo remoto di dispositivi connessi in rete tramite proxy multipli, dotato di un’interfaccia web moderna, interattiva e reattiva. Progettato per offrire un controllo granulare e in tempo reale delle connessioni shell remote, Shellz si basa su un’architettura modulare e scalabile con due backend Python distinti che cooperano per garantire sicurezza, efficienza e facilità d’uso.

---

## Architettura del Sistema

### Backend Proxy

Il backend proxy gestisce tutte le connessioni di rete tramite tre proxy principali che collaborano per autenticare, gestire e controllare i dispositivi:

- **Proxy di Autenticazione**  
  Gestisce il processo di autenticazione dei dispositivi in ingresso. Durante questa fase, il dispositivo è nello stato `authenticating`. L’autenticazione si basa su IP di rete e IP locale statico del dispositivo.

- **Proxy Limbo**  
  Punto di transizione per i dispositivi autenticati, che sono pronti per essere utilizzati. Questi dispositivi sono nello stato `online`. Il proxy limbo mantiene la lista aggiornata dei dispositivi connessi, collaborando con gli altri proxy per la sincronizzazione dello stato.

- **Proxy Generale**  
  Gestisce le connessioni attive e il controllo remoto dei dispositivi. Quando un dispositivo è attivamente utilizzato, è nello stato `using`. Coordina il passaggio dei dispositivi dal proxy di autenticazione al limbo e infine alla gestione attiva.

Questi proxy lavorano in sinergia, sincronizzando lo stato dei dispositivi tramite meccanismi interni, garantendo così una gestione distribuita e scalabile.

### Backend Web

Il backend web fornisce l’interfaccia utente e le API per la gestione e il controllo delle connessioni:

- **Tecnologie:** Python (ad esempio con FastAPI o Flask) per il backend, e TypeScript, CSS, JavaScript, HTML per il frontend.
- **Comunicazione:** WebSocket per una comunicazione bidirezionale in tempo reale tra backend proxy e frontend, permettendo aggiornamenti immediati sullo stato delle connessioni e dei dispositivi.
- **Persistenza:** Database locale SQLite per la memorizzazione di configurazioni, nomi personalizzati, gruppi e stato delle connessioni, garantendo integrità e gestione concorrente dei dati.

---

## Funzionalità Principali

### Gestione Dispositivi e Gruppi

- Dispositivi identificati tramite IP locale statico e organizzati in gruppi e sottogruppi fino a 10 livelli di profondità.
- Ogni gruppo ha un nome personalizzabile (default basato sull’IP della rete).
- Visualizzazione dello stato di ogni dispositivo con indicatori chiari:
  - `authenticating`: dispositivo in fase di autenticazione.
  - `online`: dispositivo autenticato e pronto all’uso.
  - `using`: dispositivo attivamente controllato.
- Gestione delle connessioni con possibilità di pausa, terminazione e rinomina da interfaccia web.

### Pannello di Controllo Web

- **Dashboard:** panoramica generale dello stato del sistema.
- **Dashboard/Connections:** gestione avanzata di gruppi, sottogruppi e dispositivi.
- **Dashboard/Connector:** generatore di shell payload personalizzati, multi-piattaforma (Linux, Windows, macOS) e multi-metodo (nc, powershell, python, curl).
- **Connections/[connessione]:** pagina dedicata a ogni connessione identificata da un ID univoco, con possibilità di alternare la visualizzazione tra shell e schermo remoto tramite uno switch.
- **Settings:** configurazione delle porte per i proxy, range di porte per autenticazione, blacklist di porte e altre impostazioni di sistema.

### Generatore di Shell

- Interfaccia per creare comandi di reverse shell personalizzati.
- Supporto per diverse piattaforme e linguaggi di scripting.
- Utilizzo di `curl` per eseguire comandi in modo versatile e multi-piattaforma.

---

## Comunicazione e Sincronizzazione

- I proxy collaborano per aggiornare e sincronizzare lo stato dei dispositivi.
- Il backend web riceve aggiornamenti in tempo reale tramite WebSocket, mostrando informazioni sempre aggiornate all’utente.
- Persistenza dei dati gestita tramite SQLite, garantendo integrità e gestione concorrente.

---

## Sicurezza e Configurazione

- Autenticazione basata su IP di rete e IP locale statico.
- Configurazione avanzata delle porte per i vari proxy e possibilità di blacklistare porte per evitare conflitti.
- Gestione delle connessioni con possibilità di pausa e terminazione da interfaccia web.
- Nomi personalizzati per gruppi e dispositivi per una migliore organizzazione.

---

## Sistema di Installazione

Shellz include un sistema di installazione semplice e veloce tramite GitHub, che permette di installare e configurare il server web con una sola riga di comando. Durante l’installazione, il sistema chiede all’utente quale porta utilizzare per ospitare il server web, configurandolo automaticamente.

### Installazione rapida

```bash
curl -sSL https://github.com/tuo-username/shellz/install.sh | bash
