# Guida John the Ripper

Benvenuto nella documentazione ufficiale della guida a John the Ripper. Questa pagina è stata generata per GitHub Pages e contiene tutte le istruzioni per utilizzare lo strumento.

## 📌 Overview

- John the Ripper è un cracker di password veloce e supporta molteplici sistemi operativi: Unix, macOS, Windows, DOS e altri.  
  Il suo scopo principale è rilevare password deboli sui sistemi Unix, ma supporta anche una vasta gamma di altri hash (Windows, Kerberos, ecc.).

- **Funzionalità principali**  
  - Supporto per DES, MD5, SHA, NTLM, Kerberos e altro.  
  - Cracking tramite dizionario, brute force e modalità ibrida.  
  - Altamente configurabile.  
  - La versione "jumbo" supporta anche ZIP, RAR, PDF, Office, ecc.

- **Modalità di cracking**  
  - **Dizionario**: lista di parole.  
  - **Brute force**: tutte le combinazioni.  
  - **Ibrida**: dizionario + modifiche (regole).

---

## 🔧 Installazione e Configurazione

1. Vai su: https://www.openwall.com/john/
2. Scarica la versione compatibile con il tuo sistema operativo.
3. Estrai il contenuto in una cartella, es. `C:\JohnTheRipper`.
4. Su Windows, aggiungi la variabile di sistema `JOHN_HOME` con il percorso `C:\JohnTheRipper\run`.

---

## 🗃️ Estrazione HASH da ZIP/RAR

1. Apri il terminale nella cartella `run`.
2. Posizionati dove si trova l’archivio.
3. Estrai l’hash:
   ```bash
   rar2john file.rar > rar_hash.txt
   ```
4. Avvia il cracking:
   ```bash
   john rar_hash.txt
   ```
5. Mostra la password:
   ```bash
   john --show rar_hash.txt
   ```

---

## 🧪 Kali Linux – Cracking MD5

1. Crea `hash.txt` con hash MD5 (uno per riga):
   ```
   5f4dcc3b5aa765d61d8327deb882cf99
   098f6bcd4621d373cade4e832627b4f6
   ```

2. Decomprimi la wordlist:
   ```bash
   sudo gzip -d /usr/share/wordlists/rockyou.txt.gz
   ```

3. Avvia cracking:
   ```bash
   john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
   ```

4. Mostra i risultati:
   ```bash
   john --show --format=raw-md5 hash.txt
   ```

5. Visualizza `.pot`:
   ```bash
   cat ~/.john/john.pot
   ```

6. Solo hash:password:
   ```bash
   cut -d: -f1,2 ~/.john/john.pot
   ```

7. Salva output:
   ```bash
   john --show --format=raw-md5 hash.txt > risultati.txt
   ```

---

## ⚙️ Comandi di base

```bash
john <file_hash>
john --wordlist=password.lst <file_hash>
john --show <file_hash>
Ctrl + C   # Interrompe
john --restore
```

---

## 🔁 Modalità di Cracking

```bash
john --wordlist=password.lst --rules <file_hash>
john --incremental <file_hash>
john --wordlist=password.lst --rules=Jumbo <file_hash>
```

---

## 📦 Estrazione Hash da Archivi

```bash
zip2john file.zip > zip_hash.txt
rar2john file.rar > rar_hash.txt
john zip_hash.txt
```

---

## 🚀 Opzioni Avanzate

```bash
john --format=bcrypt <file_hash>
john --fork=4 <file_hash>
john --incremental=all <file_hash>
john --wordlist=password.lst --rules <file_hash>
```

---

## 🧭 Stato e Restore

```bash
john --status
john --restore
```

---

## 📊 Analisi dei Risultati

```bash
john --show <file_hash>
john --show --pot=output.pot <file_hash>
cat ~/.john/john.pot
cut -d: -f1,2 ~/.john/john.pot
```