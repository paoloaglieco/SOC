#Scenario 
Tentativo di Reverse Shell da parte di un avversario sulla rete locale e rilevamento,analisi e blocca tramite SNORT


![Alt Text](https://github.com/paoloaglieco/SOC/blob/main/Snort/Scenario_2/sniff.png)

#Procedimento 
Attivazione modalita promiscua di SNORT tramite il comando sudo snort -dev -l


sudo: Questo comando permette di eseguire il programma con privilegi elevati (di amministratore). Snort necessita di questi privilegi perché deve accedere alle interfacce di rete a basso livello.

snort: È il programma principale di Snort, un sistema di rilevamento delle intrusioni (IDS). Avviandolo, Snort inizia a monitorare il traffico di rete.

-d: Questo parametro indica a Snort di catturare e registrare anche i dati del livello applicativo (il contenuto del pacchetto). Non solo gli header dei pacchetti, ma anche i dati veri e propri inviati all'interno di essi.

-e: Snort registrerà anche i dati del livello di collegamento, cioè gli header Ethernet. Questo consente di vedere dettagli di basso livello, come gli indirizzi MAC.

-v: Questa opzione mette Snort in modalità verbosa, cioè mostrerà in tempo reale i dettagli di ogni pacchetto catturato direttamente nel terminale.

-l .: Questo parametro indica a Snort di salvare i file di log nella directory corrente (. significa la cartella in cui ti trovi al momento dell'esecuzione del comando). Verrà creata una sottodirectory chiamata log, dove saranno memorizzati i dati catturati.

#Analisi dei log


Individuazione di una porta anomala 4444 solitamente utilizzate per le reverse shell in metasploit

![Alt Text](https://github.com/paoloaglieco/SOC/blob/main/Snort/Scenario_2/port4444.png)
![Alt Text](https://github.com/paoloaglieco/SOC/blob/main/Snort/Scenario_2/pkg_port4444.png)

#Remediation 
Creazione regola snort e attuazione della stessa per impedire la reverse shell
Comando utilizzati
sudo nano /etc/snort/rules/local.rules
sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth01 -A full

![Alt Text](https://github.com/paoloaglieco/SOC/blob/main/Snort/Scenario_2/rule.png)









