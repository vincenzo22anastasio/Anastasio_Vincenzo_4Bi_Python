## Comandi utilizzati
cd Documents
mkdir esercizio-percorsi
cd esercizio-percorsi
mkdir dati
mkdir risultati
cd dati
cd ../risultati
Get-Location

## Output
PS Z:\> cd ~                                                                                                             C:\Users\vincenzo.anastasio> cd Documents
PS C:\Users\vincenzo.anastasio\Documents> mkdir esercizio-percorsi


    Directory: C:\Users\vincenzo.anastasio\Documents


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        14/09/2026     10:58                esercizio-percorsi


PS C:\Users\vincenzo.anastasio\Documents> cd esercizio-percorsi
PS C:\Users\vincenzo.anastasio\Documents\esercizio-percorsi> mkdir dati
>> mkdir risultati


    Directory: C:\Users\vincenzo.anastasio\Documents\esercizio-percorsi


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        14/09/2026     10:58                dati
d-----        14/09/2026     10:58                risultati


PS C:\Users\vincenzo.anastasio\Documents\esercizio-percorsi> cd dati
PS C:\Users\vincenzo.anastasio\Documents\esercizio-percorsi\dati> cd ../risultati
>>
PS C:\Users\vincenzo.anastasio\Documents\esercizio-percorsi\risultati> Get-Location
>>

Path
----
C:\Users\vincenzo.anastasio\Documents\esercizio-percorsi\risultati
