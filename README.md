# Il carrello della spesa e le crisi geopolitiche

Come le crisi geopolitiche degli ultimi dieci anni si sono riflesse sui prezzi di sette prodotti
del carrello in Italia, dal 2015 al 2026.

Il caso più evidente è l'olio di girasole: dopo l'invasione dell'Ucraina il suo prezzo al consumo
è salito di **circa il 57% in cinque mesi**. Altre crisi, anche molto seguite dai media, hanno
lasciato i prezzi alimentari quasi invariati.

![Animazione: il prezzo dell'olio di girasole in Italia e sul mercato mondiale dal 2016 al 2026, con le principali crisi](figure/girasole_storico.gif)

*Olio di girasole: prezzo al consumo in Italia (linea scura) e prezzo mondiale in euro (linea chiara),
media 2025 = 100. Il prezzo mondiale reagisce subito all'invasione; quello italiano lo segue
dopo uno o due mesi e scende più lentamente.*

[Risultati](#risultati) · [Notebook](notebooks/) · [Dataset pulito](data_market/processed/dataset_mensile.csv) · [Limiti](#limiti-dellanalisi)

---

## In breve

- L'invasione dell'Ucraina è stata la crisi con l'effetto maggiore sul carrello: dodici mesi dopo,
  al netto dell'andamento che i prezzi avrebbero avuto comunque, latte circa +20 punti,
  zucchero +50–55, pane +14–17.
- Le crisi raggiungono i prezzi al consumo soprattutto attraverso l'energia, con ritardi che vanno
  da circa un mese (carburanti) a quasi un anno (caffè).
- Un alto rischio geopolitico, da solo, non fa salire i prezzi: conta quali materie prime e quali
  rotte commerciali una crisi colpisce.

## La domanda

Come sono cambiati i prezzi del carrello in Italia durante le crisi geopolitiche, dal 2015 a oggi?

Più in dettaglio: attraverso quali canali una crisi lontana arriva ai prezzi al consumo
(materie prime, energia, fertilizzanti, trasporti) e con quale ritardo. L'analisi confronta i prezzi
italiani di sette prodotti (pane, pasta, olio di girasole, caffè, zucchero, latte, carburanti)
con le materie prime mondiali, il costo dell'energia, il cambio euro/dollaro e un indice di
rischio geopolitico.

## Struttura dell'analisi

Quattro notebook trasformano cinque fonti ufficiali in un dataset mensile unico
(gennaio 2015 – ottobre 2026, 142 mesi e 33 serie) e lo analizzano.

```mermaid
flowchart LR
    A[ISTAT · FAO · Banca Mondiale<br/>BCE · Geopolitical Risk Index] --> B[01 Pulizia<br/>dataset mensile]
    B --> C[02 Esplorazione<br/>grafici e crisi]
    C --> D[03 Correlazioni<br/>e ritardi]
    D --> E[04 Modello<br/>regressioni ed event study]
```

| Notebook | Contenuto | Output |
|---|---|---|
| [01_pulizia](notebooks/01_pulizia.ipynb) | unione delle 5 fonti, indici ISTAT portati in base 2025 | `dataset_mensile.csv` |
| [02_esplorazione](notebooks/02_esplorazione.ipynb) | prezzi, variazioni su 12 mesi e rischio geopolitico nel tempo | grafici con le date delle crisi |
| [03_correlazioni](notebooks/03_correlazioni.ipynb) | legami tra prezzi e materie prime, e relativi ritardi | heatmap dei ritardi |
| [04_modello](notebooks/04_modello.ipynb) | regressioni con controlli ed event study | stime dell'effetto delle crisi |

## Risultati

### Quanto ha pesato la crisi ucraina?

Effetto stimato dodici mesi dopo l'invasione, sottraendo l'aumento che ci sarebbe stato comunque:

| Prodotto | Effetto dopo 12 mesi (punti) |
|---|---|
| Zucchero | +50–55 |
| Olio di girasole | +22–45 |
| Latte | circa +20 |
| Pane | +14–17 |
| Pasta | +9–19 |

Lo zucchero è il prodotto con l'effetto più ampio. Gli intervalli dipendono da come si definisce
l'andamento "normale" (vedi [Limiti](#limiti-dellanalisi)). Le altre crisi analizzate
(Covid, Gaza, Mar Rosso, dazi USA) non hanno avuto effetti paragonabili sui prodotti alimentari.

![Event study: effetto delle crisi sui prezzi rispetto all'andamento normale 2016–2019](figure/event_study.png)

*Scostamento dei prezzi, mese per mese, dall'andamento che avrebbero avuto crescendo come nel
2016–2019 (mese 0 = inizio della crisi). Effetti marcati compaiono solo con l'Ucraina, per gli
alimentari, e con l'Iran, per i carburanti.*

### Olio di girasole

L'Ucraina è tra i principali esportatori mondiali di olio di girasole. Con l'invasione e il blocco
dei porti del Mar Nero il prezzo mondiale è salito subito; quello italiano lo ha seguito in uno o
due mesi, con un aumento di circa il 57% in cinque mesi.

- Tenendo conto di materia prima, energia e fertilizzanti, rimane un effetto aggiuntivo di circa
  29 punti nell'anno successivo all'invasione. Possibili spiegazioni: scarsità del prodotto
  importato dall'Ucraina e acquisti di scorte nella primavera 2022.
- Il prezzo è legato più al rischio geopolitico dell'Ucraina (correlazione 0,59) che a quello
  globale (0,23).

### Il ruolo dell'energia

![Prezzi italiani e materie prime mondiali in euro, 2015–2026](figure/prezzi_vs_materie_prime.png)

*I prezzi italiani (linea nera) seguono le materie prime mondiali, ma in modo attenuato e con ritardo.*

Nei modelli di regressione il prezzo del gas europeo è significativo per 4 prodotti su 6
(pane, pasta, zucchero, latte). Per la pasta, tenendo fermo il gas, l'effetto stimato del grano
scende a meno della metà. I fertilizzanti contano per i prodotti più vicini alla produzione
agricola (zucchero, olio di girasole, latte); i trasporti non risultano significativi.

### Ritardi tra materie prime e prezzi al consumo

![Heatmap delle correlazioni tra prezzi italiani e materie prime per ritardo in mesi](figure/heatmap_ritardi.png)

*Ogni riga è un prodotto, ogni colonna un ritardo in mesi; la ★ indica il ritardo con il legame più forte.*

| Prodotto | Ritardo dalla materia prima | Correlazione |
|---|---|---|
| Carburanti | circa 1 mese | 0,89 |
| Pasta | circa 7 mesi | 0,82 |
| Latte | circa 8 mesi | 0,73 |
| Pane | circa 10 mesi | 0,75 |
| Caffè | circa 11 mesi | 0,84 |

I carburanti si adeguano quasi subito; il caffè impiega quasi un anno, anche perché i torrefattori
acquistano il caffè verde con largo anticipo. Lo zucchero italiano segue poco il mercato mondiale.

### Rischio geopolitico e prezzi

Il Geopolitical Risk Index registra picchi anche in periodi senza rincari (fine 2015, inizio 2020,
Gaza 2023). Per tutti i prodotti la correlazione con la materia prima è più alta di quella con il
rischio globale, anche concedendo a entrambi lo stesso ritardo. Il rischio legato ai paesi
produttori è invece più informativo: per pane e pasta la correlazione con il rischio della Russia
è 0,70 e 0,60, contro 0,37 e 0,15 per il rischio globale.

### Aumenti rapidi, discese lente

Dopo il picco del 2022 grano e girasole mondiali sono tornati indietro; pane, pasta e latte sono
rimasti sui livelli raggiunti. Solo i prodotti più vicini alla materia prima (olio di girasole,
zucchero) sono in parte scesi.

### La guerra in Iran (2026)

In otto mesi i carburanti sono saliti di circa 25–32 punti oltre il loro andamento normale, più che
con l'Ucraina e nonostante i tagli delle accise. Sui prodotti alimentari l'effetto non è ancora
visibile: con ritardi di 7–11 mesi, l'analisi andrà aggiornata.

### Fattori non geopolitici

Il rincaro più forte del caffè (2025) non è legato a una crisi, ma al prezzo mondiale della Robusta.
Il grano era in aumento già nel 2021, prima della guerra. Il taglio delle accise del 22 marzo 2022
si riconosce nei dati: i carburanti scendono il mese successivo al primo picco.

## Metodo

- **Correlazioni sulle variazioni, non sui livelli.** Latte italiano e rischio geopolitico degli USA
  hanno correlazione 0,53 sui livelli e −0,05 sulle variazioni: sui livelli emergono legami
  apparenti dovuti solo a una tendenza comune.
- **Regressioni con controlli.** Ogni prodotto è spiegato da materia prima (con ritardo lungo e di
  un mese), energia, trasporti, fertilizzanti e una variabile per l'anno successivo all'invasione.
- **Event study.** Ogni crisi diventa il "mese 0" e si misura lo scostamento del prezzo
  dall'andamento atteso.

<details>
<summary>Dettagli tecnici</summary>

- Indici ISTAT NIC (Ecoicop 2) portati in base 2025 = 100 con i coefficienti di raccordo ufficiali
  (2015 da base 2010, 2016–2025 da base 2015).
- Materie prime convertite da dollari a euro con il cambio medio mensile BCE.
- Variazioni percentuali su 12 mesi, per eliminare tendenza e stagionalità.
- Ritardi scelti come quelli con la correlazione più alta tra 0 e 18 mesi.
- Regressioni OLS con errori standard HAC (Newey-West), 12 ritardi, per tenere conto della
  sovrapposizione tra variazioni su 12 mesi.
- Event study con due definizioni dell'andamento normale: tendenza dei 12 mesi precedenti l'evento
  e crescita media 2016–2019.

</details>

## Come riprodurre l'analisi

```
git clone https://github.com/emamercadante03-sketch/carrello-crisi-geopolitiche.git
cd carrello-crisi-geopolitiche
python -m venv .venv
.venv\Scripts\activate          # su Mac/Linux: source .venv/bin/activate
pip install -r requirements.txt
```

Poi eseguire i notebook della cartella `notebooks/` in ordine, da `01_pulizia` a `04_modello`.

## Limiti dell'analisi

> [!NOTE]
> Per pasta e olio di girasole l'effetto della guerra è riportato come intervallo, perché dipende
> da come si stima l'andamento che i prezzi avrebbero avuto senza la crisi. Per i carburanti,
> nel caso dell'Ucraina, il risultato è troppo incerto per essere riportato.

**Dati**
- **Grano duro non disponibile**: il Pink Sheet della Banca Mondiale non riporta il grano duro
  (quello della pasta); si usa il grano tenero US HRW come approssimazione.
- **2015 incompleto**: pane, olio di girasole e caffè sono segmenti ISTAT introdotti dal 2016.
- **Ultimo mese provvisorio**: ottobre 2026 è una stima ISTAT; pane, olio di girasole e caffè non
  sono ancora disponibili per quel mese.
- **Iran non coperto dal Geopolitical Risk Index**; l'indice dell'Arabia Saudita resta basso anche
  durante la crisi di Hormuz, quindi il rischio nel Golfo è misurato solo indirettamente.
- **Punto di vista occidentale del GPR**: l'indice si basa su giornali americani e britannici.

**Metodo**
- **Eventi sovrapposti**: Gaza e Mar Rosso sono troppo vicini per separarne gli effetti; le finestre
  dei dazi USA e della guerra dei 12 giorni comprendono la guerra in Iran.
- **Periodi "normali" non normali**: l'effetto della guerra è calcolato con due definizioni del
  "normale", la tendenza dei 12 mesi precedenti l'invasione (che include i rincari post-Covid) e la
  crescita media 2016–2019, precedente al Covid. Per pasta e olio di girasole i due metodi danno
  risultati diversi, da cui gli intervalli.
- **Variazioni su 12 mesi sovrapposte**: tendono ad aumentare le correlazioni (nei modelli si usano
  errori standard HAC).
- **Ritardi scelti come i migliori tra 19**: le correlazioni corrispondenti sono leggermente
  ottimistiche, e i ritardi vanno letti come valori indicativi.
- **L'effetto aggiuntivo della guerra è una misura residua**: comprende tutto ciò che materie prime
  ed energia non spiegano nell'anno successivo all'invasione, senza identificarne la causa.

### Cosa ho imparato

- **La preparazione dei dati richiede tempo.** Il CSV dell'ISTAT codificava gli apostrofi in un modo
  che impediva la lettura, e i dati erano espressi in tre basi diverse (2010, 2015, 2025), da
  ricollegare con i coefficienti ufficiali.
- **I dati possono segnalare ciò che manca.** Un picco del rischio geopolitico a metà 2025 non
  corrispondeva a nessuna crisi dell'elenco: era la guerra dei 12 giorni tra Israele e Iran,
  poi aggiunta all'analisi.
- **Ogni metodo va verificato sui casi limite.** Prolungando la tendenza precedente, Gaza sembrava
  aver ridotto il prezzo dello zucchero di 56 punti: in realtà la tendenza "normale" era quella della
  crisi ucraina. Da qui il confronto con un periodo stabile (2016–2019).

## Sviluppi futuri

- Difference-in-differences sui carburanti Italia–USA per la guerra in Iran, con le accise come
  controllo (`misure_fiscali.csv`, da completare per il 2026)
- Previsione dei prezzi con machine learning
- Aggiornamento dell'analisi dell'Iran 2026 sugli alimentari quando saranno disponibili più mesi

## Fonti e contatti

| Fonte | Contenuto |
|---|---|
| ISTAT – NIC (Ecoicop 2) | prezzi al consumo per prodotto, mensili |
| FAO Food Price Index | prezzi mondiali del cibo |
| Geopolitical Risk Index (Caldara & Iacoviello) | tensioni geopolitiche, mensili |
| World Bank Pink Sheet | prezzi delle materie prime |
| BCE | cambio euro/dollaro |

I dati originali sono in `data_market/raw/` e non vengono modificati; il dataset pulito è
[`data_market/processed/dataset_mensile.csv`](data_market/processed/dataset_mensile.csv).

<details>
<summary>Fonti delle date delle crisi</summary>

| Evento | Data | Fonte |
|---|---|---|
| Occupazione russa della Crimea | 2014-02-27 | [Wikipedia](https://it.wikipedia.org/wiki/Annessione_della_Crimea_alla_Russia) |
| Covid-19 dichiarato pandemia dall'OMS | 2020-03-11 | [SkyTG24](https://tg24.sky.it/salute-e-benessere/2026/03/11/covid-pandemia-oms-anniversario) |
| Invasione russa dell'Ucraina | 2022-02-24 | [Wikipedia](https://it.wikipedia.org/wiki/Invasione_russa_dell%27Ucraina_del_2022) |
| Fine dell'accordo sul grano del Mar Nero | 2023-07-17 | [SkyTG24](https://tg24.sky.it/mondo/2023/07/17/accordo-grano-russia-ucraina) |
| Attacco di Hamas e inizio della guerra a Gaza | 2023-10-07 | [Wikipedia](https://it.wikipedia.org/wiki/Attacco_di_Hamas_a_Israele_del_2023) |
| Inizio degli attacchi Houthi nel Mar Rosso | 2023-11-19 | [Aspenia](https://aspeniaonline.it/non-solo-houthi-attorno-al-mar-rosso-una-crisi-multilivello/) |
| Dazi USA del Liberation Day | 2025-04-02 | [Corriere della Sera](https://www.corriere.it/economia/finanza/26_aprile_02/i-dazi-a-un-anno-dal-liberation-day-cosa-e-cambiato-per-l-economia-usa-e-cosa-dicono-i-numeri-044a71f1-ac7d-4a49-b203-6d0f692a6xlk.shtml) |
| Guerra dei 12 giorni tra Israele e Iran | 2025-06-13 | [LaPresse](https://www.lapresse.it/esteri/2025/06/24/iran-la-guerra-dei-12-giorni-dallattacco-di-israele-alla-tregua-annunciata-da-trump/) |
| Attacco di USA e Israele all'Iran | 2026-02-28 | [SkyTG24](https://tg24.sky.it/mondo/2026/02/28/guerra-iran-usa-israele-precedente) |

</details>

**Autore:** Emanuele Mercadante – [LinkedIn](https://www.linkedin.com/in/emanuele-mercadante-274180333/)
