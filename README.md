# music-school-calendar

[English](#english) | [Italiano](#italiano)

---

<a id="english"></a>

# English

A single-page app (`index.html`) to manage lessons in a music school: teachers, students, instruments, rooms, calendar, make-up lessons, teacher payments and monthly reports.

- One file. No server, no libraries, no network requests.
- Data stays in your browser. Nothing is sent anywhere.
- Italian and English, light and dark theme, desktop and mobile.

Live version: <https://sivabenepoivediamo.github.io/music-school-calendar/>
License: MIT. This repository is a GitHub template.

## Quick start

1. Open the live version, or download `index.html` and open it in a browser.
2. Click the grey "School Name" at the top left and type the name of your institution. Enter confirms, Esc cancels.
3. Add data in this order: **Instruments**, **Rooms** (optional), **Teachers**, **Students**.
4. In **Calendar**, click a day to create a lesson.

## The top bar

- Tabs: Calendar, Teachers, Students, Instruments, Rooms, Lessons, Hours.
- Teacher filter (shown when there are two or more teachers): limits everything to one teacher.
- `⤓ JSON` and `⤓ PDF`: export. `⤒`: import.
- `IT` / `EN`: language. `◐`: light or dark theme. Both choices are remembered.

## The tabs

**Calendar.** Month view, weeks start on Monday. Click a day or `+` to add a lesson; click a lesson to edit it. Markers: `€` paid, `↺` make-up, `*` student with disability. Border color: green = done, red = absent. On phones the grid becomes a list.

**Teachers.** First name, last name, rate per lesson, and a second rate for students with disability (if left empty it equals the first). Click the instrument buttons to say what each teacher teaches. Rates can be edited in the table.

**Students.** First name, last name, age, instruments, teacher, room, disability flag. `✎ Lessons` edits many lessons of a student at once (see Bulk edit).

**Instruments, Rooms.** Simple lists. Click a room name to rename it.

**Lessons.** All lessons, newest first. Absent lessons that still need a make-up are listed at the top. The paid checkbox can be changed here.

**Hours.** Monthly totals. Per teacher: hours done, planned, paid, to pay, amount due, amount paid. Per student: hours planned, done, absent, still to make up.

Deleting a teacher or a student also deletes their lessons. Every delete asks for confirmation.

## Lessons

**Create.** Click a day, choose student (teacher and room are filled in from the student), date, time (default 15:00), duration (default 60 min), status and notes. "Repeat (weeks)" creates the same lesson on the following weeks, up to 52. A repeated series can be deleted all at once.

**Status.** Planned, Done or Absent. When the app opens, any Planned lesson dated before today becomes Done automatically. Set it to Absent if the student did not come.

**Make-up.** An Absent lesson appears under "Make-ups due". Click `Make up` to create a new lesson for the same student, teacher, room and duration, linked to the absent one. Deleting the absent lesson also deletes its make-up.

**Payments.** A lesson costs the teacher's rate, or the disability rate if the student is flagged. Marking a lesson as paid saves its price at that moment; later rate changes do not alter it. In **Hours**, `Pay month` marks all done lessons of the month as paid.

**Bulk edit.** `✎ Lessons` in the Students tab. Choose which lessons (all, from today on, until yesterday), then fill in only the fields to change. Empty fields stay as they are.

## Export and import

- **JSON** contains all your data. Use it for backups and to move data to another browser or device. Importing replaces the current data after confirmation.
- **PDF** covers the month shown: a calendar page, then a report with teachers and amounts, hours per student, the lesson list and the make-ups still due. It follows the teacher filter. Characters outside Latin-1 print as `?`.
- Both file names start with the institution name.

## Where data is stored

- In the browser's local storage, saved after every change.
- Data belongs to one browser on one device and one web address. Another browser, a private window or a different address shows empty data.
- Clearing the browser's site data deletes it. Export a JSON backup regularly.
- There are no accounts, no sync and no shared editing. To share data, export and import the JSON.
- Student data is personal data. It stays on the device, and the institution is responsible for who can access that device.

## For developers

**Customize `index.html`**

- Currency: change `CUR` (for example `'USD'`).
- Colors: CSS variables at the top (`:root` light, `:root[data-t=dark]` dark).
- Default time and duration of a lesson: `openL()`.
- Texts: `DICT`, one object per language. The default institution name is the `brand` key.
- New language: add its locale to `LOC`, add a full copy of the `it` object to `DICT` translated (every key is required), and add a button inside `<span class="lg">` in the header. Month names, weekdays and number formats come from the browser.

**Publish your copy on GitHub Pages**

1. Click **Use this template** to create your repository.
2. Edit `index.html` and commit.
3. In **Settings > Pages**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. The page appears at `https://<user>.github.io/<repository>/`.

Publishing the page does not publish data: each visitor has their own data in their own browser.

Storage keys are `acad` (data), `acadT` (theme), `acadL` (language). All pages of one GitHub account share the same `<user>.github.io` storage, so if you publish several apps or copies under one account, rename these keys to avoid clashes.

**Data format** (JSON export)

```json
{
  "name": "",
  "teachers":    [{ "id": "", "name": "", "surname": "", "rate": 0, "rateD": 0, "iids": [] }],
  "students":    [{ "id": "", "name": "", "surname": "", "age": 0, "iids": [], "tid": "", "aid": "", "dis": false }],
  "instruments": [{ "id": "", "name": "" }],
  "rooms":       [{ "id": "", "name": "" }],
  "lessons":     [{ "id": "", "sid": "", "tid": "", "aid": "", "date": "YYYY-MM-DD", "time": "HH:MM",
                    "dur": 60, "st": "planned", "paid": false, "amt": 0, "note": "", "mk": "", "rid": "" }]
}
```

`iids` are instrument ids; `sid`, `tid`, `aid` are student, teacher and room ids. `st` is `planned`, `done` or `absent`. `mk` is the id of the absent lesson a make-up replaces, `rid` identifies a repeated series, `amt` is the price saved when the lesson was paid.

**License.** MIT. Keep the copyright and license notice (`LICENSE` file) when you copy or modify the project.

---

<a id="italiano"></a>

# Italiano

Un'app in una sola pagina (`index.html`) per gestire le lezioni di una scuola di musica: insegnanti, alunni, strumenti, aule, calendario, recuperi, pagamenti agli insegnanti e resoconti mensili.

- Un solo file. Nessun server, nessuna libreria, nessuna richiesta di rete.
- I dati restano nel tuo browser. Non viene inviato nulla all'esterno.
- Italiano e inglese, tema chiaro e scuro, desktop e mobile.

Versione online: <https://sivabenepoivediamo.github.io/music-school-calendar/>
Licenza: MIT. Questo repository è un template GitHub.

## Primi passi

1. Apri la versione online, oppure scarica `index.html` e aprilo in un browser.
2. Clicca il "Nome Scuola" grigio in alto a sinistra e scrivi il nome della tua istituzione. Invio conferma, Esc annulla.
3. Inserisci i dati in quest'ordine: **Strumenti**, **Aule** (facoltativo), **Insegnanti**, **Alunni**.
4. In **Calendario**, clicca un giorno per creare una lezione.

## La barra in alto

- Schede: Calendario, Insegnanti, Alunni, Strumenti, Aule, Lezioni, Ore.
- Filtro insegnante (compare con due o più insegnanti): limita tutto a un solo insegnante.
- `⤓ JSON` e `⤓ PDF`: esporta. `⤒`: importa.
- `IT` / `EN`: lingua. `◐`: tema chiaro o scuro. Entrambe le scelte vengono ricordate.

## Le schede

**Calendario.** Vista mensile, la settimana inizia di lunedì. Clicca un giorno o `+` per aggiungere una lezione; clicca una lezione per modificarla. Simboli: `€` retribuita, `↺` recupero, `*` alunno con disabilità. Colore del bordo: verde = svolta, rosso = assente. Sul telefono la griglia diventa un elenco.

**Insegnanti.** Nome, cognome, tariffa per lezione e una seconda tariffa per alunni con disabilità (se vuota è uguale alla prima). Clicca i pulsanti degli strumenti per indicare cosa insegna ciascuno. Le tariffe si modificano nella tabella.

**Alunni.** Nome, cognome, età, strumenti, insegnante, aula, indicazione di disabilità. `✎ Lezioni` modifica insieme molte lezioni di un alunno (vedi Modifica multipla).

**Strumenti, Aule.** Semplici elenchi. Clicca il nome di un'aula per rinominarla.

**Lezioni.** Tutte le lezioni, dalla più recente. In alto ci sono le lezioni assenti che aspettano ancora un recupero. Qui si può cambiare la casella di retribuzione.

**Ore.** Totali del mese. Per insegnante: ore svolte, previste, retribuite, da retribuire, importo da pagare, importo pagato. Per alunno: ore previste, svolte, assenti, ancora da recuperare.

Eliminare un insegnante o un alunno elimina anche le sue lezioni. Ogni eliminazione chiede conferma.

## Lezioni

**Creare.** Clicca un giorno, scegli l'alunno (insegnante e aula si compilano dalla sua scheda), data, ora (predefinita 15:00), durata (predefinita 60 min), stato e note. "Ripeti (settimane)" crea la stessa lezione nelle settimane successive, fino a 52. Una serie ripetuta si può eliminare tutta insieme.

**Stato.** Prevista, Svolta o Assente. All'apertura dell'app, ogni lezione Prevista con data precedente a oggi diventa Svolta in automatico. Se l'alunno non è venuto, impostala come Assente.

**Recupero.** Una lezione Assente compare in "Recuperi da fare". Con `Recupera` si crea una nuova lezione con stesso alunno, insegnante, aula e durata, collegata a quella assente. Eliminando la lezione assente si elimina anche il suo recupero.

**Pagamenti.** Una lezione costa la tariffa dell'insegnante, oppure quella per disabilità se l'alunno è indicato come tale. Segnando una lezione come retribuita si salva il suo prezzo di quel momento; le successive variazioni di tariffa non lo cambiano. In **Ore**, `Retribuisci mese` segna come retribuite tutte le lezioni svolte del mese.

**Modifica multipla.** `✎ Lezioni` nella scheda Alunni. Scegli quali lezioni (tutte, da oggi in poi, fino a ieri), poi compila solo i campi da cambiare. I campi vuoti restano com'erano.

## Esportazione e importazione

- Il **JSON** contiene tutti i dati. Serve per le copie di sicurezza e per spostare i dati su un altro browser o dispositivo. L'importazione sostituisce i dati attuali, dopo conferma.
- Il **PDF** riguarda il mese visualizzato: una pagina con il calendario, poi un resoconto con insegnanti e importi, ore per alunno, elenco delle lezioni e recuperi ancora da fare. Segue il filtro insegnante. I caratteri fuori da Latin-1 vengono stampati come `?`.
- I nomi di entrambi i file iniziano con il nome dell'istituzione.

## Dove sono salvati i dati

- Nella memoria locale del browser, a ogni modifica.
- I dati appartengono a un browser, su un dispositivo, a un indirizzo web. Un altro browser, una finestra privata o un indirizzo diverso mostrano dati vuoti.
- Cancellare i dati del sito dal browser li elimina. Esporta regolarmente una copia JSON.
- Non ci sono account, sincronizzazione né modifica condivisa. Per condividere i dati, esporta e importa il JSON.
- I dati degli alunni sono dati personali. Restano sul dispositivo, e l'istituzione è responsabile di chi può accedervi.

## Per gli sviluppatori

**Personalizzare `index.html`**

- Valuta: modifica `CUR` (ad esempio `'USD'`).
- Colori: variabili CSS all'inizio (`:root` chiaro, `:root[data-t=dark]` scuro).
- Ora e durata predefinite di una lezione: `openL()`.
- Testi: `DICT`, un oggetto per lingua. Il nome predefinito dell'istituzione è la chiave `brand`.
- Nuova lingua: aggiungi il locale a `LOC`, aggiungi a `DICT` una copia completa e tradotta dell'oggetto `it` (servono tutte le chiavi) e aggiungi un pulsante dentro `<span class="lg">` nell'intestazione. Nomi di mesi, giorni e formati numerici vengono dal browser.

**Pubblicare la tua copia con GitHub Pages**

1. Clicca **Use this template** per creare il tuo repository.
2. Modifica `index.html` e fai il commit.
3. In **Settings > Pages** scegli **Deploy from a branch**, ramo `main`, cartella `/ (root)`.
4. La pagina compare su `https://<utente>.github.io/<repository>/`.

Pubblicare la pagina non pubblica i dati: ogni visitatore ha i propri dati nel proprio browser.

Le chiavi di salvataggio sono `acad` (dati), `acadT` (tema), `acadL` (lingua). Tutte le pagine di uno stesso account GitHub condividono la memoria di `<utente>.github.io`: se pubblichi più app o più copie con lo stesso account, rinomina queste chiavi per evitare conflitti.

**Formato dei dati** (esportazione JSON)

```json
{
  "name": "",
  "teachers":    [{ "id": "", "name": "", "surname": "", "rate": 0, "rateD": 0, "iids": [] }],
  "students":    [{ "id": "", "name": "", "surname": "", "age": 0, "iids": [], "tid": "", "aid": "", "dis": false }],
  "instruments": [{ "id": "", "name": "" }],
  "rooms":       [{ "id": "", "name": "" }],
  "lessons":     [{ "id": "", "sid": "", "tid": "", "aid": "", "date": "AAAA-MM-GG", "time": "HH:MM",
                    "dur": 60, "st": "planned", "paid": false, "amt": 0, "note": "", "mk": "", "rid": "" }]
}
```

`iids` sono gli id degli strumenti; `sid`, `tid`, `aid` sono gli id di alunno, insegnante e aula. `st` vale `planned`, `done` o `absent`. `mk` è l'id della lezione assente che un recupero sostituisce, `rid` identifica una serie ripetuta, `amt` è il prezzo salvato quando la lezione è stata retribuita.

**Licenza.** MIT. Mantieni l'avviso di copyright e di licenza (file `LICENSE`) quando copi o modifichi il progetto.
