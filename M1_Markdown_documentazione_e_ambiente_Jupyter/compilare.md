# Esercizio 2 — Istruzioni di compilazione con elenchi, comandi e citazioni

Per compilare ed eseguire un programma Java a partire da un repository appena clonato, è utile seguire una procedura ordinata e verificabile passo per passo.

1. Apri il terminale nel progetto appena clonato e controlla la struttura delle cartelle:

   ```bash
   cd ~/Documents/progetto-java
   ls -la
   find src -maxdepth 2 -type f
   ```

2. Verifica che la classe principale sia presente e che il file sorgente si trovi nella cartella `src/`:

   ```bash
   grep -R "class MediaVoti" src/
   ```

3. Compila il codice Java in una cartella di output dedicata, ad esempio `bin/`:

   ```bash
   mkdir -p bin
   javac -d bin src/MediaVoti.java
   ```

   In questo passaggio, il file `MediaVoti.java` viene trasformato in bytecode Java pronto per l'esecuzione.

4. Esegui il programma dalla cartella di output appena creata:

   ```bash
   cd bin
   java MediaVoti
   ```

5. Se il programma richiede input, lo inserisci da terminale e controlli il risultato finale:

   - verifica che i dati siano corretti
   - controlla che il programma abbia terminato senza errori
   - salva eventuali output utili per la documentazione

> Errore: `'javac'` non è riconosciuto come comando interno o esterno, un programma eseguibile oppure un file batch.
>
> Questo accade quando il JDK non è installato o non è stato aggiunto al `PATH` di sistema. Per risolvere il problema, installa il JDK e riapri il terminale.

Il comando `javac` va sempre usato prima di `java`: il primo compila i sorgenti, il secondo esegue la classe già compilata.
