# Kritis Print: example output

Kritis Print first works out which print sales are worth comparing, then uses them, together with auction estimates and the sales history of the same plate, to place any price in the market.

![How Kritis Print handles one lot: sort out what it is, find the same plate's sales, place a price on a ladder](how-it-works.svg)

*One real lot, three steps. Artwork image via WikiArt (fair use), © Zao Wou-Ki; sales data from public auction results.*

## What it does

1. **Sorts out what the object is.** Auction records mix signed editions, proofs, reproductions and pages taken from books. Only signed limited editions and proofs are priced; anything else is set aside with the reason stated.
2. **Finds the same plate.** It identifies the plate from the catalogue raisonné number or the edition details and gathers every recorded sale of it.
3. **Places a price on a ladder.** A floor, a typical range and a ceiling, from which any asking price, at auction, in a gallery or online, gets a plain answer: unusually low, cheap, normal or above the ceiling.

## One lot, end to end

Zao Wou-Ki, *Montagnes et soleil* (1951), lithograph, signed, numbered 192/200, Ågerup 59. Dobiaschofsky, Bern, sale of 6 November 2026. Estimate CHF 2,000–3,000 (about US$2,500–3,750).

The tool's output, registered on 1 November 2026, before the sale (key fields, USD):

```json
{
  "object_class": "signed_limited",
  "plate": "zao_wou_ki:Agerup:59",
  "edition": { "number": "192", "size": 200, "signed": true },
  "same_plate_last_3_years": { "sales": 6, "median_usd": 3331 },
  "floor": 2500,
  "ceiling": 4754,
  "cheap_below": 2125,
  "unusually_low_below": 1250
}
```

In plain words. This plate has sold 19 times at auction since 2014, between US$3,300 and US$10,300 until 2022 and at a median of US$3,331 over the last three years. For this sale the expected range is US$2,500 to US$4,754. A price below US$2,125 is cheap; below US$1,250 is unusual enough to check the sheet and the listing before anything else.

## A live test, recorded before the results

Twelve Zao Wou-Ki prints offered at eight auction houses between 4 and 21 November 2026. The ranges were fixed before the sales; results are added as each sale is reported, and nothing else in the table changes.

![Price ranges recorded for twelve live lots](live-test-2026-11.svg)

| Closes | Lot | House | Estimate (USD) | Floor | Ceiling | Result |
| --- | --- | --- | --- | --- | --- | --- |
| 4 Nov | *La Cathédrale* 2/50 | Freeman's \| Hindman, New York | 4,000–6,000 | 3,531 | 8,255 | pending |
| 6 Nov | *Montagnes et soleil* Å.59, 192/200 | Dobiaschofsky, Bern | 2,500–3,750 | 2,500 | 4,754 | pending |
| 6 Nov | *Ohne Titel* Å.150, 82/125 | Dobiaschofsky, Bern | 2,500–3,750 | 2,500 | 4,754 | pending |
| 7 Nov | *Rivière* 189 (= Å.192), H.C. | Sturies, Düsseldorf | 3,510 | 2,808 | 5,340 | pending |
| 7 Nov | *Rivière* 220, *Canto Pisan* 45/50 | Sturies, Düsseldorf | 1,755 | 1,404 | 2,670 | pending |
| 7 Nov | *Rivière* 244, 78/95 | Sturies, Düsseldorf | 2,340 | 1,872 | 3,560 | pending |
| 7 Nov | *Rivière* 246, 75/95 | Sturies, Düsseldorf | 1,755 | 1,404 | 2,670 | pending |
| 9 Nov | Å.260, unsigned etching, ed. 125 | Alyes, Hong Kong (online) | 1,400–1,750 | not priced | not priced | pending |
| 10 Nov | *Sans titre* Å.192, 64/95 | Swann, New York | 3,500–4,500 | 2,825 | 6,604 | pending |
| 11 Nov | Untitled aquatint, 49/100 | DEWIT, Ostend | 4,680–5,850 | 3,718 | 8,693 | pending |
| 13 Nov | Å.328, ed. 99, foxing | Mainichi, Tokyo | 3,300–4,620 | 3,168 | 6,024 | pending |
| 21 Nov | *Composition* 38/125 | Schramm, Kiel | 1,123–1,404 | 1,264 | 2,543 | pending |

The unsigned etching was set aside rather than priced. Prices include the buyer's premium and are converted to US dollars on the sale date.

## Notes

- Developed on Zao Wou-Ki prints; collection now covers more artists and auction houses.
- A market reference for comparable sales, not an appraisal of a single sheet. It does not judge condition or authenticity.
- The source code and data are private.

[Back to the project overview](../../projects/kritis-print.md)
