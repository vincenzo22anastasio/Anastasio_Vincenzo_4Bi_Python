# Esercizio 11 — Che cosa stampa un notebook eseguito fuori ordine

## 1. Ordine reale di esecuzione

Il notebook mostra le celle nel seguente ordine di scrittura: `[2]`, `[4]`, `[3]`, `[1]`, ma questo non è l'ordine eseguito dal kernel. L'ordine di esecuzione si deduce dai dati prodotti dalle celle e dal fatto che la cella `[3]` usa la variabile `posti` prima di essere modificata nella cella `[4]`.

L'ordine reale, se il kernel parte da uno stato vuoto e le celle vengono eseguite come appaiono nell'editor, è:

1. `[2]` → inizializza `aula` e `posti`
2. `[4]` → modifica `posti` e stampa `22`
3. `[3]` → usa `posti` e `iscritti` nello stesso momento
4. `[1]` → definisce `iscritti`

L'ordine di scrittura non coincide con l'ordine di esecuzione, e la prova è proprio nel fatto che la cella `[3]` ha calcolato `posti - iscritti` usando `posti = 24` mentre la cella `[4]` ha poi mostrato `22`.

## 2. Perché la cella [4] mostra 22 e la cella [3] ha usato 24

La cella `[4]` esegue la riga:

```python
posti = posti - 2
print("Posti disponibili:", posti)
```

Questa modifica avviene dopo che la cella `[3]` ha già valutato `posti - iscritti` come `24 - 22 = 2`. Per questo motivo la cella `[3]` stampa:

```text
Laboratorio 3 - liberi: 2
```

ma la cella `[4]` stampa:

```text
Posti disponibili: 22
```

## 3. Output previsto dopo `Restart Kernel and Run All Cells`

Se il notebook viene eseguito dall'alto verso il basso in ordine di visualizzazione, il kernel esegue le celle in questo ordine:

```text
[2]  aula = "Laboratorio 3"
     posti = 24
[4]  posti = posti - 2
     print("Posti disponibili:", posti)
     Posti disponibili: 22
[3]  print(aula, "-", "liberi:", posti - iscritti)
     NameError: name 'iscritti' is not defined
```

La cella `[1]`, che definisce `iscritti`, non verrebbe eseguita perché la cella `[3]` genera un errore prima di arrivare a quella parte del notebook.

## 4. Cella che causa l'errore

La cella che produce l'errore è la `[3]`:

```python
print(aula, "-", "liberi:", posti - iscritti)
```

Messaggio esatto:

```text
NameError: name 'iscritti' is not defined
```

## 5. Come correggere il notebook

Per far sì che il notebook arrivi in fondo senza errori, occorre far sì che la variabile `iscritti` sia definita prima della cella `[3]`. Il modo più semplice è inserire la cella `[1]` all'inizio del notebook, oppure riscrivere le celle in un ordine logico:

```python
iscritti = 22
print("Iscritti:", iscritti)

aula = "Laboratorio 3"
posti = 24

print(aula, "-", "liberi:", posti - iscritti)

posti = posti - 2
print("Posti disponibili:", posti)
```

Con questa disposizione, il valore che comparirà al posto di `liberi: 2` sarà:

```text
Laboratorio 3 - liberi: 2
```

e il notebook verrà eseguito senza errori anche da un kernel appena avviato.
