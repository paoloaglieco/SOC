#Scenario 1
Sniffing dei pacchetti dati tramite Snort e creazione regola che ferma l'attacco bruteforce

#Procedimento
1-Modalità promiscua di Snort tramite il comando sudo snort -dev -l .
sudo: Questo comando permette di eseguire il programma con privilegi elevati (di amministratore). Snort necessita di questi privilegi perché deve accedere alle interfacce di rete a basso livello.

snort: È il programma principale di Snort, un sistema di rilevamento delle intrusioni (IDS). Avviandolo, Snort inizia a monitorare il traffico di rete.

-d: Questo parametro indica a Snort di catturare e registrare anche i dati del livello applicativo (il contenuto del pacchetto). Non solo gli header dei pacchetti, ma anche i dati veri e propri inviati all'interno di essi.

-e: Snort registrerà anche i dati del livello di collegamento, cioè gli header Ethernet. Questo consente di vedere dettagli di basso livello, come gli indirizzi MAC.

-v: Questa opzione mette Snort in modalità verbosa, cioè mostrerà in tempo reale i dettagli di ogni pacchetto catturato direttamente nel terminale.

-l .: Questo parametro indica a Snort di salvare i file di log nella directory corrente (. significa la cartella in cui ti trovi al momento dell'esecuzione del comando). Verrà creata una sottodirectory chiamata log, dove saranno memorizzati i dati catturati.

Di seguito lo screen che riporta che siamo stati in ascolto per 46 secondi e i pacchetti intercettati

![Alt Text](https://github.com/paoloaglieco/SOC/blob/main/Snort/Scenario_1/sniffing_mode.png)

2- Analisi del log prodotto da SNORT

comando utilizzato sudo snort file.pcap 'port 22'
sudo snort file.pcap 'port 80'

Dalle le analisi preliminari si evince che un host sta utilizzando la connessione sulla porta 80 e tentando diversi accessi sulla porta 22 sul server ssh

![Alt Text](https://github.com/paoloaglieco/SOC/blob/main/Snort/Scenario_1/port80.png)
![Alt Text](https://github.com/paoloaglieco/SOC/blob/main/Snort/Scenario_1/port22.png)

Dato il conseguente e anomalo traffico sulla porta 22 si puo ipotizzare che l'attacante stia procendo tramite script automatici ad un attacco brute force sul server ssh

#Remediation

Creazione di una regola SNORT che blocca sull'immediato l'attacco e ci permette in futuro di poter migliorare la nostra postura

![Alt Text](https://github.com/paoloaglieco/SOC/blob/main/Snort/Scenario_1/rule.png)

Comandi utilizzati sudo nano /etc/snort/rules/rules.local

















