# Esercizio 15 — Notebook riproducibile e pulito prima del commit

## 1. Definizione del problema

Un notebook è riproducibile quando, dopo un riavvio del kernel e l'esecuzione di tutte le celle con `Kernel > Restart Kernel and Run All Cells`, termina senza errori e produce gli stessi risultati attesi.

Per dimostrare il problema, si può creare un notebook con questa sequenza di celle:

```python
# Cell A
numero = 5
```

```python
# Cell B
print(numero + 3)
```

Se poi si cancella la cella che definisce `numero` senza riavviare il kernel, la cella successiva continua a funzionare in quel momento perché il valore è ancora presente in memoria. Tuttavia, la situazione non è più riproducibile: se il kernel viene riavviato, la variabile non esiste più e l'esecuzione completa fallisce.

## 2. Verifica della rottura della riproducibilità

Dopo aver cancellato la cella di definizione, senza riavviare il kernel, il notebook sembra ancora funzionare a schermo. Il problema emerge con il riavvio del kernel:

```text
NameError: name 'numero' is not defined
```

Il messaggio indica che la cella che si ferma è la cella B, perché tenta di usare una variabile che non è più definita nello stato iniziale del notebook.

## 3. Correzione del notebook

Per correggere il problema, si reinserisce la cella che assegna la variabile prima della cella che la utilizza:

```python
# Cell A
numero = 5
```

```python
# Cell B
print(numero + 3)
```

Dopo aver fatto questa correzione, si esegue `Kernel > Restart Kernel and Run All Cells` e il notebook termina correttamente senza errori.

## 4. Commit e pulizia degli output

Una volta corretto, il notebook va aggiunto al repository con gli output salvati:

```bash
git add M1_jupyter/M1_esercizio10.ipynb
git commit -m "Aggiungo notebook dell'esercizio 10"
```

Poi si puliscono gli output in place:

```bash
jupyter nbconvert --clear-output --inplace M1_jupyter/M1_esercizio10.ipynb
```

E infine si crea un secondo commit:

```bash
git add M1_jupyter/M1_esercizio10.ipynb
git commit -m "Pulisce output del notebook prima del commit"
```

## 5. Confronto fra i due commit

Per confrontare le modifiche dei due commit si usa:

```bash
git diff --shortstat HEAD~1 HEAD
```

oppure, se si desidera il dettaglio completo:

```bash
git diff --numstat HEAD~1 HEAD
```

Il primo commit conserva gli output del notebook, mentre il secondo commit elimina i risultati eseguiti e lascia solo il codice. Per questo motivo il numero di righe cambiate è diverso: il primo commit è più grande perché contiene anche i risultati generati, mentre il secondo è più leggero perché pulisce gli output.

## 6. Ignorare i salvataggi automatici di Jupyter

Per evitare che la cartella dei checkpoint compaia tra i file non tracciati, si aggiungono queste righe al file `.gitignore`:

```gitignore
# Jupyter checkpoints
.ipynb_checkpoints/
**/.ipynb_checkpoints/
```

Dopo questa modifica, il comando:

```bash
git status
```

non deve più mostrare la cartella dei salvataggi automatici di Jupyter tra i file non tracciati.

## 7. Conclusione

La riproducibilità di un notebook dipende dalla presenza di tutte le celle necessarie nello stato iniziale del kernel. Se una variabile viene definita in una cella e poi rimossa senza riavviare il kernel, l'output può sembrare corretto a schermo ma fallisce dopo un riavvio. Il controllo con `Restart Kernel and Run All Cells` è il modo corretto per verificare che il notebook sia davvero pronto per essere versionato e consegnato.
