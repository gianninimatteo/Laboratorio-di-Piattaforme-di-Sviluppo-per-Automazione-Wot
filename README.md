# Progetto WoT - Riscaldamento automatizzato

### Obiettivo del progetto

L'obiettivo del progetto è avere sensori di temperatura in più stanze, esposti come “Things” WoT, in modo che client WoT possano leggere i dati, ricevere eventi e controllare il riscaldamento in modo standardizzato.


### Funzionalità previste

- Monitoraggio in tempo reale della temperatura in ogni stanza

- Controllo del riscaldamento tramite impostazione della temperatura desiderata.

- Notifica di eventi quando si cambia la temperatura desiderata in ogni stanza.

- Automazione semplice del riscaldamento in base ai valori misurati. Ogni stanza ha un termostato che si accende/spegne in base alla temperatura.


### Architettura del sistema

- **Things** (dispositivi WoT)

  - Sensori di temperatura (uno per stanza).

  - Sistema di riscaldamento (attuatore).

- **Client WoT**

  - Dashboard web per visualizzazione e controllo delle temperature

  - Motore di automazione per applicare le regole (decide cosa fare in base ai dati dei sensori)

  - Visualizzazione in tempo reale dei valori e degli eventi


Ogni Thing espone una Thing Description (TD) che definisce:

- **Properties**

  - temperature: (temperatura attuale della stanza)

  - targetTemperature: (temperatura desiderata che si vuole far raggiungere alla stanza)

  Se temperature < targetTemperature → accende il riscaldamento.

  Se temperature ≥ targetTemperature → spegne il riscaldamento.

- **Actions**

  - setTargetTemperature(x): è l’azione che permette di modificare targetTemperature

  - turnOn(), turnOff() : accende e spegne il riscaldamento
 
  - Il riscaldamento parte quando un sensore rileva -0.1 rispetto alla temperatura desiderata (es: 19.9°C se Temp. desiderata = 20°C), mentre        per lo spegnimento c'è un margine di 0.3 (es. si spegne se Temp. desiderata = 20 °C e il termostato arriva a 20.3 °C).

- **Events**

  - temperature change : quando si cambia una temperatura desiderata in una stanza.
    

 ### Comunicazione

- Protocolli Web: HTTP e MQTT

- I client WoT interagiscono leggendo le Thing Description, scoprendo automaticamente le funzionalità dei dispositivi


### Tecnologie utilizzate

- Backend / Things: Node.js, node-wot, Typescript

- Frontend: HTML, CSS, Javascript

- Protocolli: HTTP, MQTT
  

# Passaggi Installazione
### Windows
- Installa Node.js
- Vai sul sito *https://mosquitto.org/download/*
- Scarica la versione **mosquitto-2.1.2-install-windows-x64.exe**
- Dopo l’installazione apri Powershell come amministratore e digita: **net start mosquitto**
 (potrebbe dire che il servizio è già avviato).
- Vai su visual studio code, apri il progetto e da terminale fai:
  
  • **npm install**

  • **npx tsc**
  
  • **node dist/things/heater.js**
  
- Poi apri un secondo terminale senza chiudere quello di prima e fai: **node dist/things/sensors.js**
- Poi apri un terzo terminale senza chiudere quello di prima e fai: **node dist/heating-logic.js**
- Poi direttamente dalla cartella apri il file **dashboard.html**

### macOS
- Installa Node.js
- Da terminale digita: **brew install mosquitto**
- Avvia il broker Mosquitto: **brew services start mosquitto**
- Vai su visual studio code, apri il progetto e da terminale fai:
  
  • **npm install**

  • **npx tsc**
  
  • **node dist/things/heater.js**
  
- Poi apri un secondo terminale senza chiudere quello di prima e fai: **node dist/things/sensors.js**
- Poi apri un terzo terminale senza chiudere quello di prima e fai: **node dist/heating-logic.js**
- Poi direttamente dalla cartella apri il file **dashboard.html**
