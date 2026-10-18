# Music School Calendar

[English](#english) | [Italiano](#italiano)

---

<a id="english"></a>

# English

A single-page app (`index.html`) to manage a music school: teachers, students, instruments, rooms, calendar, make-up lessons, teacher compensation, student payments, balance and monthly reports.

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
5. In **Payments**, set the default enrollment and lesson fees.

## The top bar

- Tabs: Calendar, Teachers, Students, Instruments, Rooms, Lessons, Hours, Payments, Balance.
- Teacher filter (shown when there are two or more teachers): limits the views to one teacher. It does not apply to Balance, which always covers the whole school.
- `⤓ JSON` and `⤓ PDF`: export. `⤒`: import.
- `IT` / `EN`: language. `◐`: light or dark theme. Both choices are remembered.

## The tabs

**Calendar.** Month view, weeks start on Monday. Click a day or `+` to add a lesson; click a lesson to edit it. Markers: `€` paid to the teacher, `↺` make-up, `*` student with disability. Border color: green = done, red = absent. On phones the grid becomes a list.

**Teachers.** First name, last name, rate per lesson, and a second rate for students with disability (if left empty it equals the first). Click the instrument buttons to say what each teacher teaches. Rates can be edited in the table.

**Students.** First name, last name, age, instruments, teacher, room, disability flag. `✎ Lessons` edits many lessons of a student at once (see Bulk edit).

**Instruments, Rooms.** Simple lists. Click a room name to rename it.

**Lessons.** All lessons, newest first. Absent lessons that still need a make-up are listed at the top. Two checkboxes can be changed here: *Paid* (the teacher has been paid) and *Received* (the student has paid).

**Hours.** Monthly totals. Per teacher: hours done, planned, paid, to pay, amount due, amount paid. Per student: hours planned, done, absent, still to make up.

**Payments.** Money coming in from students. See [Payments](#payments).

**Balance.** Income and expenses with the final result. See [Balance](#balance).

Deleting a teacher or a student also deletes their lessons. Every delete asks for confirmation.

## Lessons

**Create.** Click a day, choose student (teacher and room are filled in from the student), date, time (default 15:00), duration (default 60 min), status and notes. "Repeat (weeks)" creates the same lesson on the following weeks, up to 52. A repeated series can be deleted all at once.

**Status.** Planned, Done or Absent. When the app opens, any Planned lesson dated before today becomes Done automatically. Set it to Absent if the student did not come.

**Make-up.** An Absent lesson appears under "Make-ups due". Click `Make up` to create a new lesson for the same student, teacher, room and duration, linked to the absent one. Deleting the absent lesson also deletes its make-up.

**Teacher compensation.** A lesson costs the teacher's rate, or the disability rate if the student is flagged. Absent lessons are not counted. Marking a lesson as *Paid* saves its price at that moment; later rate changes do not alter it. In **Hours**, `Pay month` marks all done lessons of the month as paid.

**Student payments.** Each lesson also has a *Received* flag, set in the Lessons tab, in the lesson dialog, in Bulk edit or from the Payments tab. See [Payments](#payments).

**Bulk edit.** `✎ Lessons` in the Students tab. Choose which lessons (all, from today on, until yesterday), then fill in only the fields to change. Empty fields stay as they are.

## Payments

Two separate fees, both customizable.

- **Default fees.** One enrollment fee and one lesson fee for the whole school. They start at 0.
- **Per-student override.** Each student can have a different enrollment fee and lesson fee. An empty field means "use the default".

**Enrollments.** One row per student: fee, *Received* checkbox, amount received, amount to receive, enrollment date. The date decides in which period the fee appears in the Balance. For students that already existed before this feature, it is set to their first lesson.

**Lessons.** Month view. One row per student: lesson fee, number of lessons, amount received, amount to receive.

- Done and planned lessons are charged. Absent lessons are not.
- Received lessons keep the price they had when they were collected; later fee changes do not alter them.
- `Collect done` marks the done, not yet received lessons of the month as received. It appears only when planned lessons are also outstanding.
- `Collect all` marks all lessons of the month, done and planned, as received.
- Each button exists per student and, in the total row, for all students. Both ask for confirmation.

## Balance

Choose **Month**, **Year** or **All**.

| | Items |
|---|---|
| **Income** | Enrollments, lesson fees, other income |
| **Expenses** | Compensation (one line per teacher), other expenses |

Every item has three columns: **Actual** (already received or paid), **Pending** (still to receive or to pay) and **Total**. The **Balance** table shows the result for each column.

- Enrollments are placed in the period of the enrollment date. Lessons, both fees and compensation, are placed in the period of the lesson date.
- Teacher compensation is *Actual* when the lesson is marked Paid, *Pending* otherwise.
- **Other items** are your own entries: date, description, income or expense, amount. Add rental, materials, grants and so on. They count as actual, and can be edited or deleted in the table.

## Export and import

- **JSON** contains all your data: school, people, lessons, default fees, student fees and payments, and other income and expenses. Use it for backups and to move data to another browser or device. Importing replaces the current data after confirmation. Files exported by older versions can be imported; missing fields are filled with defaults.
- **PDF** covers the month shown: a calendar page, then a report with teachers and amounts, instruments, hours per student, the lesson list, the make-ups still due, then **Payments** (per student: enrollment received and to receive, lessons, amount received and to receive) and **Balance** (income, expenses, result, other items). Payments follow the teacher filter; the balance always covers the whole school. Characters outside Latin-1 print as `?`.
- Both file names start with the institution name.

## Where data is stored

- In the browser's local storage, saved after every change.
- Data belongs to one browser on one device and one web address. Another browser, a private window or a different address shows empty data.
- Clearing the browser's site data deletes it. Export a JSON backup regularly.
- There are no accounts, no sync and no shared editing. To share data, export and import the JSON.
- Student and financial data is sensitive. It stays on the device, and the institution is responsible for who can access that device.

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
  "fees":        { "enr": 0, "les": 0 },
  "teachers":    [{ "id": "", "name": "", "surname": "", "rate": 0, "rateD": 0, "iids": [] }],
  "students":    [{ "id": "", "name": "", "surname": "", "age": 0, "iids": [], "tid": "", "aid": "", "dis": false,
                    "enr": "", "fee": "", "enrD": "YYYY-MM-DD", "enrP": false, "enrA": 0 }],
  "instruments": [{ "id": "", "name": "" }],
  "rooms":       [{ "id": "", "name": "" }],
  "lessons":     [{ "id": "", "sid": "", "tid": "", "aid": "", "date": "YYYY-MM-DD", "time": "HH:MM",
                    "dur": 60, "st": "planned", "paid": false, "amt": 0, "rc": false, "ramt": 0,
                    "note": "", "mk": "", "rid": "" }],
  "entries":     [{ "id": "", "date": "YYYY-MM-DD", "type": "in", "desc": "", "amt": 0 }]
}
```

- `iids` are instrument ids; `sid`, `tid`, `aid` are student, teacher and room ids.
- `st` is `planned`, `done` or `absent`. `mk` is the id of the absent lesson a make-up replaces, `rid` identifies a repeated series.
- `paid` and `amt`: the teacher has been paid, and the price saved at that moment.
- `rc` and `ramt`: the student has paid the lesson, and the fee saved at that moment.
- `fees`: default enrollment (`enr`) and lesson (`les`) fees.
- Student `enr` and `fee`: custom enrollment and lesson fee; an empty string means "use the default".
- Student `enrD`, `enrP`, `enrA`: enrollment date, enrollment received, and the fee saved when it was received.
- `entries`: other income and expenses. `type` is `in` or `out`.

**License.** MIT. Keep the copyright and license notice (`LICENSE` file) when you copy or modify the project.

---

<a id="italiano"></a>

# Italiano

Un'app in una sola pagina (`index.html`) per gestire una scuola di musica: insegnanti, alunni, strumenti, aule, calendario, recuperi, compensi agli insegnanti, pagamenti degli alunni, bilancio e resoconti mensili.

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
5. In **Pagamenti**, imposta le quote predefinite di iscrizione e di lezione.

## La barra in alto

- Schede: Calendario, Insegnanti, Alunni, Strumenti, Aule, Lezioni, Ore, Pagamenti, Bilancio.
- Filtro insegnante (compare con due o più insegnanti): limita le viste a un solo insegnante. Non vale per il Bilancio, che riguarda sempre tutta la scuola.
- `⤓ JSON` e `⤓ PDF`: esporta. `⤒`: importa.
- `IT` / `EN`: lingua. `◐`: tema chiaro o scuro. Entrambe le scelte vengono ricordate.

## Le schede

**Calendario.** Vista mensile, la settimana inizia di lunedì. Clicca un giorno o `+` per aggiungere una lezione; clicca una lezione per modificarla. Simboli: `€` retribuita all'insegnante, `↺` recupero, `*` alunno con disabilità. Colore del bordo: verde = svolta, rosso = assente. Sul telefono la griglia diventa un elenco.

**Insegnanti.** Nome, cognome, tariffa per lezione e una seconda tariffa per alunni con disabilità (se vuota è uguale alla prima). Clicca i pulsanti degli strumenti per indicare cosa insegna ciascuno. Le tariffe si modificano nella tabella.

**Alunni.** Nome, cognome, età, strumenti, insegnante, aula, indicazione di disabilità. `✎ Lezioni` modifica insieme molte lezioni di un alunno (vedi Modifica multipla).

**Strumenti, Aule.** Semplici elenchi. Clicca il nome di un'aula per rinominarla.

**Lezioni.** Tutte le lezioni, dalla più recente. In alto ci sono le lezioni assenti che aspettano ancora un recupero. Qui si possono cambiare due caselle: *Retribuita* (l'insegnante è stato pagato) e *Incassata* (l'alunno ha pagato).

**Ore.** Totali del mese. Per insegnante: ore svolte, previste, retribuite, da retribuire, importo da pagare, importo pagato. Per alunno: ore previste, svolte, assenti, ancora da recuperare.

**Pagamenti.** Il denaro in entrata dagli alunni. Vedi [Pagamenti](#pagamenti).

**Bilancio.** Entrate e uscite con il risultato finale. Vedi [Bilancio](#bilancio).

Eliminare un insegnante o un alunno elimina anche le sue lezioni. Ogni eliminazione chiede conferma.

## Lezioni

**Creare.** Clicca un giorno, scegli l'alunno (insegnante e aula si compilano dalla sua scheda), data, ora (predefinita 15:00), durata (predefinita 60 min), stato e note. "Ripeti (settimane)" crea la stessa lezione nelle settimane successive, fino a 52. Una serie ripetuta si può eliminare tutta insieme.

**Stato.** Prevista, Svolta o Assente. All'apertura dell'app, ogni lezione Prevista con data precedente a oggi diventa Svolta in automatico. Se l'alunno non è venuto, impostala come Assente.

**Recupero.** Una lezione Assente compare in "Recuperi da fare". Con `Recupera` si crea una nuova lezione con stesso alunno, insegnante, aula e durata, collegata a quella assente. Eliminando la lezione assente si elimina anche il suo recupero.

**Compensi agli insegnanti.** Una lezione costa la tariffa dell'insegnante, oppure quella per disabilità se l'alunno è indicato come tale. Le lezioni assenti non vengono contate. Segnando una lezione come *Retribuita* si salva il suo prezzo di quel momento; le successive variazioni di tariffa non lo cambiano. In **Ore**, `Retribuisci mese` segna come retribuite tutte le lezioni svolte del mese.

**Pagamenti degli alunni.** Ogni lezione ha anche un'indicazione *Incassata*, modificabile nella scheda Lezioni, nella finestra della lezione, nella Modifica multipla o dalla scheda Pagamenti. Vedi [Pagamenti](#pagamenti).

**Modifica multipla.** `✎ Lezioni` nella scheda Alunni. Scegli quali lezioni (tutte, da oggi in poi, fino a ieri), poi compila solo i campi da cambiare. I campi vuoti restano com'erano.

## Pagamenti

Due quote separate, entrambe personalizzabili.

- **Quote predefinite.** Una quota di iscrizione e una quota per lezione, valide per tutta la scuola. Partono da 0.
- **Personalizzazione per alunno.** Ogni alunno può avere una quota di iscrizione e una quota per lezione diverse. Un campo vuoto significa "usa la quota predefinita".

**Iscrizioni.** Una riga per alunno: quota, casella *Incassata*, importo ricevuto, importo da ricevere, data di iscrizione. La data decide in quale periodo la quota compare nel Bilancio. Per gli alunni già presenti prima di questa funzione è impostata alla data della loro prima lezione.

**Lezioni.** Vista mensile. Una riga per alunno: quota per lezione, numero di lezioni, importo ricevuto, importo da ricevere.

- Si addebitano le lezioni svolte e previste. Le assenti no.
- Le lezioni incassate mantengono il prezzo che avevano al momento dell'incasso; le successive variazioni di quota non lo cambiano.
- `Incassa svolte` segna come incassate le lezioni svolte del mese non ancora incassate. Compare solo se ci sono anche lezioni previste da incassare.
- `Incassa tutte` segna come incassate tutte le lezioni del mese, svolte e previste.
- Ogni pulsante esiste per alunno e, nella riga del totale, per tutti gli alunni. Entrambi chiedono conferma.

## Bilancio

Scegli **Mese**, **Anno** o **Totale**.

| | Voci |
|---|---|
| **Entrate** | Iscrizioni, quote lezioni, altre entrate |
| **Uscite** | Compensi (una riga per insegnante), altre uscite |

Ogni voce ha tre colonne: **Effettivo** (già ricevuto o pagato), **In sospeso** (ancora da ricevere o da pagare) e **Totale**. La tabella **Saldo** mostra il risultato per ciascuna colonna.

- Le iscrizioni vanno nel periodo della data di iscrizione. Le lezioni, sia le quote sia i compensi, vanno nel periodo della data della lezione.
- Il compenso di un insegnante è *Effettivo* se la lezione è segnata Retribuita, *In sospeso* altrimenti.
- Le **Altre voci** sono inserite da te: data, descrizione, entrata o uscita, importo. Servono per affitto, materiali, contributi e così via. Contano come effettive e si modificano o eliminano nella tabella.

## Esportazione e importazione

- Il **JSON** contiene tutti i dati: scuola, persone, lezioni, quote predefinite, quote e pagamenti degli alunni, altre entrate e uscite. Serve per le copie di sicurezza e per spostare i dati su un altro browser o dispositivo. L'importazione sostituisce i dati attuali, dopo conferma. I file esportati da versioni precedenti si possono importare; i campi mancanti vengono riempiti con valori predefiniti.
- Il **PDF** riguarda il mese visualizzato: una pagina con il calendario, poi un resoconto con insegnanti e importi, strumenti, ore per alunno, elenco delle lezioni, recuperi ancora da fare, poi **Pagamenti** (per alunno: iscrizione ricevuta e da ricevere, lezioni, importo ricevuto e da ricevere) e **Bilancio** (entrate, uscite, saldo, altre voci). I pagamenti seguono il filtro insegnante; il bilancio riguarda sempre tutta la scuola. I caratteri fuori da Latin-1 vengono stampati come `?`.
- I nomi di entrambi i file iniziano con il nome dell'istituzione.

## Dove sono salvati i dati

- Nella memoria locale del browser, a ogni modifica.
- I dati appartengono a un browser, su un dispositivo, a un indirizzo web. Un altro browser, una finestra privata o un indirizzo diverso mostrano dati vuoti.
- Cancellare i dati del sito dal browser li elimina. Esporta regolarmente una copia JSON.
- Non ci sono account, sincronizzazione né modifica condivisa. Per condividere i dati, esporta e importa il JSON.
- I dati degli alunni e quelli economici sono sensibili. Restano sul dispositivo, e l'istituzione è responsabile di chi può accedervi.

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
  "fees":        { "enr": 0, "les": 0 },
  "teachers":    [{ "id": "", "name": "", "surname": "", "rate": 0, "rateD": 0, "iids": [] }],
  "students":    [{ "id": "", "name": "", "surname": "", "age": 0, "iids": [], "tid": "", "aid": "", "dis": false,
                    "enr": "", "fee": "", "enrD": "AAAA-MM-GG", "enrP": false, "enrA": 0 }],
  "instruments": [{ "id": "", "name": "" }],
  "rooms":       [{ "id": "", "name": "" }],
  "lessons":     [{ "id": "", "sid": "", "tid": "", "aid": "", "date": "AAAA-MM-GG", "time": "HH:MM",
                    "dur": 60, "st": "planned", "paid": false, "amt": 0, "rc": false, "ramt": 0,
                    "note": "", "mk": "", "rid": "" }],
  "entries":     [{ "id": "", "date": "AAAA-MM-GG", "type": "in", "desc": "", "amt": 0 }]
}
```

- `iids` sono gli id degli strumenti; `sid`, `tid`, `aid` sono gli id di alunno, insegnante e aula.
- `st` vale `planned`, `done` o `absent`. `mk` è l'id della lezione assente che un recupero sostituisce, `rid` identifica una serie ripetuta.
- `paid` e `amt`: l'insegnante è stato pagato, e il prezzo salvato in quel momento.
- `rc` e `ramt`: l'alunno ha pagato la lezione, e la quota salvata in quel momento.
- `fees`: quote predefinite di iscrizione (`enr`) e di lezione (`les`).
- `enr` e `fee` dell'alunno: quota di iscrizione e di lezione personalizzate; una stringa vuota significa "usa la quota predefinita".
- `enrD`, `enrP`, `enrA` dell'alunno: data di iscrizione, iscrizione incassata, e la quota salvata quando è stata incassata.
- `entries`: altre entrate e uscite. `type` vale `in` o `out`.

**Licenza.** MIT. Mantieni l'avviso di copyright e di licenza (file `LICENSE`) quando copi o modifichi il progetto.
