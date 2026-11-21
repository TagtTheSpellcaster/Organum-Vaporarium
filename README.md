# Organum Vaporarium

![Brevetto meccanico](https://img.shields.io/badge/BREVETTO%20MECCANICO-1.2-b8860b)
![Machina](https://img.shields.io/badge/Machina%20N%C2%B0-007-8a6c42)
![Anno](https://img.shields.io/badge/anno-1894-5a4632)
![Licenza](https://img.shields.io/badge/licenza-AGPL--3.0-blue)
![HTML5](https://img.shields.io/badge/HTML5-canvas-e34f26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-f7df1e?logo=javascript&logoColor=black)
![Web Audio](https://img.shields.io/badge/audio-Web%20Audio%20API-informational)
![Dipendenze](https://img.shields.io/badge/dipendenze-nessuna-brightgreen)
![File singolo](https://img.shields.io/badge/file-singolo-informational)

Gioco di memoria steampunk in un unico file HTML, nello stile del Simon: un organo a vapore con quattro canne suona una sequenza di note, che il giocatore deve ripetere. Machina N° 007 della serie OFFICINA DEGLI ENIGMI.

**BREVETTO MECCANICO 1.2 – 1894**

## Requisiti

- Un browser moderno con supporto per HTML5 Canvas e Web Audio.
- Nessuna installazione, nessuna dipendenza, nessuna risorsa esterna, nessun file audio: i suoni sono sintetizzati dal browser.

## Avvio

Aprire `organum-vaporarium.html` nel browser (doppio clic, oppure `File > Apri`). Con un server statico qualsiasi funziona allo stesso modo:

```
python3 -m http.server 8000
```

e poi `http://localhost:8000/organum-vaporarium.html`.

Il browser attiva l'audio solo dopo un'azione dell'utente: il suono parte al primo clic, tocco o tasto premuto.

## Come si gioca

- Premere **AVVIA IL CONCERTO**. L'organo suona una nota; ripeterla premendo la canna corrispondente (o il tasto sotto di essa).
- A ogni turno la sequenza si allunga di una nota. Non c'è un numero massimo di turni.
- Ogni nota sbagliata fa perdere un punto di pressione alla caldaia (3 in tutto, mostrati dal manometro) e la sequenza viene riascoltata. Al terzo errore la caldaia si scarica e la partita finisce.
- Il record conserva il turno più alto completato ed è salvato nel browser.
- Con il pulsante **MODO LIBERO** si suona senza regole.
- Suonare è possibile anche prima di avviare la partita.
- La velocità di riproduzione aumenta con i turni fino a un limite: la durata della nota scende da 0,54 s a 0,30 s (dal turno 13) e la pausa fra le note da 0,19 s a 0,12 s (dal turno 10).

### Comandi

| Azione | Mouse / tocco | Tastiera |
|--------|---------------|----------|
| Canna 1 (SOL) | clic sulla colonna | `1` oppure `A` |
| Canna 2 (DO) | clic sulla colonna | `2` oppure `S` |
| Canna 3 (MI) | clic sulla colonna | `3` oppure `D` |
| Canna 4 (DO acuto) | clic sulla colonna | `4` oppure `F` |

La nota dura finché il tasto o il dito restano premuti. Il tocco multiplo è supportato.

## Le canne

| Canna | Nota | Frequenza | Lunghezza relativa | Metallo |
|-------|------|-----------|--------------------|---------|
| 1 | SOL | 196,2 Hz | 1 | rame |
| 2 | DO | 261,6 Hz | 3/4 | ottone |
| 3 | MI | 327,0 Hz | 3/5 | acciaio |
| 4 | DO acuto | 523,3 Hz | 3/8 | bronzo patinato |

Le note formano il secondo rivolto dell'accordo di DO maggiore, come nel Simon originale (SOL – DO – MI – DO), in intonazione giusta: le frequenze stanno nel rapporto 3 : 4 : 5 : 8. La lunghezza di ogni canna è inversamente proporzionale alla frequenza, come in un organo reale.

## Suoni

- Ogni nota è un'onda periodica con sei armoniche (`PeriodicWave`), filtrata passa-basso, con attacco di 50 ms.
- All'attacco si aggiungono un breve soffio di rumore filtrato attorno alla terza armonica (il "chiff" delle canne ad anima) e uno sbuffo di vapore.
- L'errore è una coppia di onde a dente di sega leggermente scordate, con sbuffo; l'esaurimento della caldaia è un glissando discendente.
- Pulsante **SUONO: ON/OFF** e cursore del volume logaritmico (da −50 dB a 0 dB). Volume e stato sono salvati nel browser.

## Dettagli tecnici

- Un unico file HTML con CSS e JavaScript inline; rendering su `<canvas>` con scala per densità di pixel.
- Le canne sono disegnate come cilindri in prospettiva dall'alto (apertura ellittica, fondo curvo, anelli e labbro con la stessa curvatura), con piede conico innestato nel piano superiore del cassone. Il cassone è disegnato con piano superiore in prospettiva, fronte con pannelli incassati e valvole, montanti d'ottone e piedini.
- Vapore, alone luminoso e manometro sono animati nel ciclo di disegno; il vapore è un sistema di particelle semplice.
- Salvataggio nel browser (`localStorage`): `ov_best`, `ov_vol`, `ov_mute`. L'accesso è protetto da `try/catch`, quindi il gioco funziona anche senza storage.

## Verifiche

- Partita completa fino al turno 15 in Chromium, alternando mouse e tastiera, senza raggiungere alcun limite.
- Tre errori consecutivi fino alla caldaia scarica; ripetizione della sequenza dopo ogni errore.
- Modo libero e riproduzione prima dell'avvio.
- Nessun errore di script.

Non verificati: ascolto del suono (timbro e volume), input touch su dispositivi reali, Safari, bilanciamento della difficoltà.

## Licenza

Distribuito con licenza GNU Affero General Public License, versione 3 (AGPL-3.0). Il testo completo è nel file `LICENSE`, da scaricare da <https://www.gnu.org/licenses/agpl-3.0.txt>. Chi ospita una versione modificata come servizio di rete deve offrire agli utenti il codice sorgente corrispondente.

## Serie

OFFICINA DEGLI ENIGMI · Machina N° 007 · BREVETTO MECCANICO 1.2 – 1894
