## Metodo Scelto
Chiave SSH.

## Appunto in più
- La Chiave SSH: È come una coppia "serratura e chiave" digitale. Una metà sta sul tuo computer e l'altra su GitHub. Una volta collegate, il computer si riconosce automaticamente senza farti inserire mai più password o codici.
- Il Token Personale HTTPS: È una password speciale (una lunghissima stringa di lettere e numeri) generata da GitHub.           Sostituisce la tua vera password dell'account e si usa ogni volta che ti viene richiesta l'autenticazione.

## Motivazione
Ho scelto la chiave SSH perché uso un computer personale: permette di collegarsi a GitHub in modo sicuro e automatico, senza dover reinserire password o token.

## Esito finale
@vincenzo22anastasio ➜ /workspaces/Anastasio_Vincenzo_4Bi_Python (main) $ ssh -T git@github.com
The authenticity of host 'github.com (140.82.121.4)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
git@github.com: Permission denied (publickey).