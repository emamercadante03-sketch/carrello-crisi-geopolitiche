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

## Stato del progetto
- [x] Fase 1 – Domanda e dati
- [x] Fase 2 – Pulizia
- [ ] Fase 3 – Esplorazione
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

## Autore
[Emanuele Mercadante] – [LinkedIn](https://www.linkedin.com/in/emanuele-mercadante-274180333/)
