# Guida John the Ripper

## Overview
- John the Ripper è un cracker di password veloce e supporta molteplici sistemi operativi, tra cui Unix, macOS, Windows, DOS e altri.
  Il suo scopo principale è rilevare password deboli sui sistemi Unix, ma supporta anche una vasta gamma di altre tipologie di hash, come quelli di Windows e Kerberos.
- Funzionalità principali
  JtR può lavorare con vari formati di hash, tra cui DES, MD5, SHA, NTLM di Windows, Kerberos, e molti altri.
  È dotato di modalità di cracking multiple, come attacchi di dizionario, brute force e modalità ibrida.
  È configurabile, quindi gli utenti possono creare e personalizzare modalità di cracking proprie, se necessario.
  John è disponibile in versione "jumbo", che aggiunge il supporto per centinaia di altri tipi di hash e algoritmi, tra cui archivi ZIP, RAR, PDF, e Microsoft Office.
- Modalità di cracking
  Modalità di dizionario: Usa una lista di parole (wordlist) per tentare di abbinare la password.
  Modalità brute force: Testa tutte le possibili combinazioni di caratteri fino a trovare quella corretta.
  Modalità ibrida: Combina un attacco di dizionario con modifiche alle parole (mangling rules) per aumentare le probabilità di successo.

## Scaricare e Configurare John the Ripper
1. Vai al sito ufficiale di John the Ripper: https://www.openwall.com/john/
2. Nella sezione "Downloads", scarica la versione corretta per il tuo sistema operativo.
   Ad esempio, per Windows, scarica il pacchetto john-xxx-win-x64.zip.
3. Estrai il contenuto del file ZIP in una cartella, ad esempio C:\JohnTheRipper. (es.in C://)
4. Aggiungi John the Ripper al Path del sistema (Questo Pc > Proprietà > Impostazioni di sistema avanzate):
   - Nella finestra che si apre, clicca su Variabili di sistema > Path > Modifica > Nuovo.
   - Aggiungi nome variabile "JOHN_HOME" e il percorso della cartella run di John the Ripper (ad esempio, C:\JohnTheRipper\run).

## Estrarre l'HASH dal File RAR e crackare la password (Eseguito con successo)
1. Apri CMD direttamente dalla cartella Run (C:\JohnTheRipper\run).
2. Seleziona la cartella del file da crackare.
3. Usa "rar2john" o "zip2john" per estrarre l'hash del file RAR o Zip. Supponiamo che il file RAR si chiami file.rar, il comando sarà:
"rar2john file.rar > rar_hash.txt"
Questo comando crea un file di testo chiamato rar_hash.txt che contiene l'hash del file RAR.
4. Cracking della password: hai lanciato John con: john.exe hash.txt
5. Visualizzazione del risultato: john.exe --show hash.txt

## Comandi di base
- Cracking di un hash:
    john <file_hash>
- Cracking con una wordlist personalizzata:
    john --wordlist=password.lst <file_hash>
- Mostrare i risultati (password trovate):
    john --show <file_hash>
- Interrompere una sesssione di cracking
    ctrl + c
- Riprendere una sessione di cracking interrotta:
    john --restore

Modalità di cracking 
- Dizionario + regole
    john --wordlist=password.lst --rules <file_hash>
- Brute Force (Incrementale):
    john --incremental <file_hash>
- Dizionario con regole avanzate:
    john --wordlist=password.lst --rules=Jumbo <file_hash>
    
Estrazione degli hash (per file ZIP, RAR, ecc.)
- Per file ZIP:
    zip2john file.zip > zip_hash.txt
- Per file RAR:
    rar2john file.rar > rar_hash.txt
- Cracking di file ZIP o RAR:
    john zip_hash.txt

Opzioni avanzate
- Specificare il formato dell’hash (es: bcrypt):
    john --format=bcrypt <file_hash>
- Cracking parallelo con più core (OpenMP):
    john --fork=4 <file_hash>
- Modalità incrementale "all":
    john --incremental=all <file_hash>
- Mangling avanzato con wordlist:
    john --wordlist=password.lst --rules <file_hash>

File di stato e report
- Stato attuale del cracking:
    john --status
Creazione automatica del file di stato (per restore):
    john --restore

Analisi dei risultati
- Visualizzazione delle password trovate:
    john --show <file_hash>
Esportare i risultati in file .pot:
    john --show --pot=output.pot <file_hash>
