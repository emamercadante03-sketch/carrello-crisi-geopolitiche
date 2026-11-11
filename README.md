# Il carrello della spesa e le crisi geopolitiche

## Domanda
Come sono cambiati i prezzi del carrello in Italia durante le crisi
geopolitiche dal 2015 a oggi?

## Prodotti analizzati
Pane, pasta, olio di semi, caffè, zucchero, latte, carburanti.
Il prezzo del petrolio (Brent) è usato come fattore esterno.

## Dati
| Fonte | Cosa contiene |
|---|---|
| ISTAT – NIC (Ecoicop 2) | Prezzi al consumo per prodotto, mensili |
| FAO Food Price Index | Prezzi mondiali del cibo |
| Geopolitical Risk Index (Caldara & Iacoviello) | Tensioni geopolitiche, mensili |
| World Bank Pink Sheet | Prezzi delle materie prime |
| BCE | Cambio euro/dollaro |
| eventi.csv | Date delle crisi considerate |

I dati originali sono in `data_market/raw/` e non vengono modificati.

### Fonti delle date degli eventi        
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
| Attacco di USA e Israele all'Iran | 2026-02-28 | [Wikipedia](https://it.wikipedia.org/wiki/Guerra_Iran-Israele_del_2025) |

## Stato del progetto
- [x] Fase 1 – Domanda e dati
- [x] Fase 2 – Pulizia
- [x] Fase 3 – Esplorazione
- [ ] Fase 4 – Correlazioni
- [ ] Fase 5 – Modello
- [ ] Fase 6 – Conclusioni

## Limiti dell'analisi
- **Grano duro non disponibile**: il Pink Sheet della Banca Mondiale non ha il prezzo
  del grano duro (quello della pasta); si usa il grano tenero US HRW come approssimazione.
- **Ultimo mese provvisorio**: ottobre 2026 è una stima ISTAT; pane, olio di girasole
  e caffè non sono ancora disponibili per quel mese.
- **Eventi sovrapposti**: la guerra a Gaza (ottobre 2023) e gli attacchi nel Mar Rosso
  (novembre 2023) sono troppo vicini per separarne gli effetti con dati mensili.
- **Effetti di lunga durata**: i rincari post-Covid erano ancora in corso all'inizio della
  guerra in Ucraina (febbraio 2022), quindi il periodo "normale" precedente è anomalo.
  - **Iran non coperto dal Geopolitical Risk Index**: l'indice per paese copre 44 paesi
  ma non l'Iran; la crisi del 2026 è misurata indirettamente tramite gli indici di
  Israele, Arabia Saudita e Stati Uniti.
- **Punto di vista occidentale del GPR**: l'indice è costruito su giornali americani e
  britannici, quindi misura il rischio geopolitico come viene raccontato in Occidente.
- **Misure fiscali 2026 incomplete** (TODO): in `misure_fiscali.csv` manca la data di
  inizio del taglio accise solo sul gasolio e la situazione dopo il 25 agosto 2026.

## Autore
[Emanuele Mercadante] – [LinkedIn](https://www.linkedin.com/in/emanuele-mercadante-274180333/)
