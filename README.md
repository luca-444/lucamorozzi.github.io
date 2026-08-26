# lucamorozzi.it

Sito personale di Luca Morozzi. Sito statico, una sola pagina, palette interamente in scala di grigi.

## Contenuto della cartella

| File | A cosa serve |
|---|---|
| `index.html` | La pagina. Contiene HTML, CSS e JavaScript in un unico file: non ci sono build step né dipendenze. |
| `404.html` | Pagina di errore, usata automaticamente da GitHub Pages. |
| `CNAME` | Dominio custom: `lucamorozzi.it`. Non rinominarlo. |
| `.nojekyll` | Dice a GitHub Pages di pubblicare i file così come sono, senza passare da Jekyll. |
| `favicon.svg` | Icona del browser (monogramma LM). |
| `robots.txt` | Istruzioni per i motori di ricerca. |
| `sitemap.xml` | Mappa del sito. Aggiorna `lastmod` quando fai modifiche importanti. |
| `portrait_grayscale.png` | Ritratto usato nella hero. |
| `banner_grayscale.jpg` | Immagine della fascia a metà pagina. |

## Come pubblicare

1. Carica tutti i file nella **root** del repository (non in una sottocartella).
2. Nel repo: **Settings → Pages → Source: Deploy from a branch**, branch `main`, cartella `/ (root)`.
3. In **Custom domain** inserisci `lucamorozzi.it` e attiva **Enforce HTTPS**.
4. Configura il DNS su Register.it come descritto sotto.

## DNS su Register.it

Il dominio è registrato su Register.it, quindi i record vanno impostati nel loro pannello.

**Dove:** login su register.it → `I tuoi prodotti` → clicca `lucamorozzi.it` → `Dominio & DNS` → `Configurazione DNS` → scegli **Gestione Avanzata**. La gestione guidata non basta: servono quattro record A con lo stesso nome e un CNAME che punta fuori dal dominio, e solo la modalità avanzata li accetta.

**Prima di aggiungere: cancella il record A esistente** sul dominio nudo. Register.it lo crea di default verso la propria pagina di parcheggio e, se resta, va in conflitto con GitHub.

Record da inserire — dominio nudo (nome `@`, o vuoto, secondo come lo chiama il pannello):

| Tipo | Nome | Valore |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Record per il `www` (opzionale ma consigliato, così anche `www.lucamorozzi.it` funziona):

| Tipo | Nome | Valore |
|---|---|---|
| CNAME | www | `<tuo-utente-github>.github.io.` |

Se vuoi anche IPv6, aggiungi quattro record AAAA su `@`: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`.

**Non toccare i record MX.** Se su questo dominio hai o vuoi la posta, quelli restano come sono: cambiare gli A non influenza l'email.

**Tempi.** Register.it dichiara fino a 24-48 ore per la propagazione. Su GitHub, in `Settings → Pages`, il campo Custom domain si popola da solo leggendo il file `CNAME` del repo; la casella **Enforce HTTPS** diventa cliccabile solo dopo che il certificato è stato emesso, quindi se all'inizio è grigia è normale — torna il giorno dopo e attivala.

**Verifica da terminale:**

```
dig +short lucamorozzi.it
```

Deve restituire i quattro IP di GitHub. Se restituisce ancora un IP di Register.it, la propagazione non è finita o il vecchio record A non è stato cancellato.

## Come modificare i contenuti

Tutto il testo è dentro `index.html`, in italiano e in chiaro. I punti che cambierai più spesso:

- **Percorso** — cerca `═══ PERCORSO`. Ogni tappa è un blocco `<article class="step">`. Per aggiungerne una copia un blocco esistente e aggiorna il numero in `step-n`.
- **Ecosistema** — cerca `id="cards"`. Ogni progetto è una `.card` con un attributo `data-c` che vale `attivo`, `testing` o `cassetto`: è quello che pilota i filtri.
- **Contatori** — cerca `data-count`. Il numero nell'attributo è il valore finale dell'animazione.
- **Contatti** — cerca `id="contatti"`.

## Vincolo di design

La palette è definita una volta sola in `:root`, all'inizio del CSS, e contiene solo grigi. Le immagini hanno `filter: grayscale(100%)` applicato a livello di documento, quindi anche caricando una foto a colori resterà in bianco e nero. Se aggiungi elementi nuovi, usa le variabili esistenti (`--ink`, `--panel`, `--line`, `--smoke`, `--ash`, `--chalk`, `--white`) invece di scrivere colori a mano.

## Font

Archivo (display, con asse di larghezza variabile), Instrument Sans (testo), IBM Plex Mono (etichette e dati). Caricati da Google Fonts.
