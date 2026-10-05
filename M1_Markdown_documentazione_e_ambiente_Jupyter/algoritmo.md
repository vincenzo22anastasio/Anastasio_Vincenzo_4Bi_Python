# Esercizio 9 — Diagramma di flusso di un algoritmo noto

L'algoritmo di ricerca sequenziale su un array è un metodo semplice ma molto utile per verificare se un valore è presente e, in caso affermativo, in quale posizione si trova. Partendo dall'inizio dell'array, si confronta ciascun elemento con il valore cercato fino a trovare una corrispondenza oppure terminare la scansione.

```java
public class RicercaSequenziale {
    public static int cerca(int[] array, int valore) {
        for (int i = 0; i < array.length; i++) {
            if (array[i] == valore) {
                return i;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] voti = {7, 6, 8, 5, 9};
        int trovato = cerca(voti, 8);
        System.out.println("Indice trovato: " + trovato);
    }
}
```

```mermaid
flowchart TD
    A([Inizio]) --> B[crea array = {7, 6, 8, 5, 9}, valore = 8, i = 0]
    B --> C{i < array.length?}
    C -- Sì --> D{array[i] == valore?}
    D -- Sì --> E[restituisci i]
    E --> F([Fine])
    D -- No --> G[i = i + 1]
    G --> C
    C -- No --> H[restituisci -1]
    H --> F
```

Se l'elemento cercato non è presente, il ciclo termina dopo aver controllato tutti gli elementi e la funzione restituisce `-1`, che indica appunto l'assenza del valore nell'array. Nel caso dell'esempio con `8`, il risultato atteso è l'indice `2`.
