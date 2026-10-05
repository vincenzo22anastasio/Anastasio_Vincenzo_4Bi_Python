# Esercizio 12 — Architettura del progetto con due diagrammi Mermaid

Il programma Java è organizzato in classi che rappresentano gli oggetti principali del dominio: `Utente`, `Libro`, `Biblioteca` e `Prenotazione`. La struttura mostra come il sistema gestisce la disponibilità dei volumi e registra le prenotazioni.

```mermaid
classDiagram
    class Utente {
        -String nome
        +Utente(String nome)
        +String getNome()
        +void prenotaLibro(Libro libro)
    }

    class Libro {
        -String titolo
        -String autore
        +Libro(String titolo, String autore)
        +String getTitolo()
        +boolean disponibile
    }

    class Prenotazione {
        -String codice
        -Utente utente
        -Libro libro
        +Prenotazione(Utente utente, Libro libro)
        +String getCodice()
    }

    class Biblioteca {
        -List~Libro~ catalogo
        -List~Utente~ utenti
        +Biblioteca()
        +void aggiungiLibro(Libro libro)
        +boolean prenota(Libro libro, Utente utente)
    }

    Biblioteca "1" *-- "0..*" Libro
    Biblioteca "1" --> "0..*" Utente
    Biblioteca "1" --> "0..*" Prenotazione
    Utente "1" --> "0..*" Prenotazione
    Prenotazione --> Libro
    Prenotazione --> Utente
```

Il diagramma `classDiagram` mostra la composizione della `Biblioteca` con i suoi libri e le relazioni con le prenotazioni. L'utente può prenotare un libro, la biblioteca verifica la disponibilità del volume e genera una prenotazione associata al libro e all'utente.

```mermaid
sequenceDiagram
    actor U as Utente
    participant B as Biblioteca
    participant L as Libro
    participant P as Prenotazione

    U->>B: prenotaLibro("Algoritmi", utente)
    B->>B: verificaDisponibilita()
    alt libro disponibile
        B->>L: controlla stato
        L-->>B: disponibile
        B->>P: creaPrenotazione(utente, libro)
        P-->>B: prenotazione creata
        B-->>U: conferma prenotazione
    else libro non disponibile
        B-->>U: rifiuta prenotazione
    end
```

Nel diagramma `sequenceDiagram` il flusso parte dall'utente, passa alla biblioteca per la verifica della disponibilità e, in caso positivo, crea una prenotazione. Il ramo `alt ... else` rappresenta la scelta tra disponibilità e indisponibilità del libro, evidenziando il comportamento del sistema in entrambi i casi.
