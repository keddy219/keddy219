# Kritis Print: example output

Kritis Print first decides which print sales are worth comparing, then combines auction-estimate calibration with same-plate sales data to give a traceable market price reference.

This page shows what it produces, using real lots and the tool's actual output. The source code and datasets remain private; the figures below are copied from the tool's output files.

![How Kritis Print handles one lot: check scope, identify the plate, set the ladder](how-it-works.svg)

*The animation follows one real lot through the three steps. Artwork image via WikiArt (fair use), © Zao Wou-Ki; sales data from public auction results.*

## What it adds to an auction estimate

An auction estimate exists only for lots at auction, and only for that one lot. Kritis Print adds three things.

1. **Which records are comparable.** Auction records mix signed editions, proofs, reproductions and pages taken from books. The tool sorts them before any price is computed, so a reproduction does not drag down the price history of an original print.
2. **The plate's own history.** It identifies the plate from the catalogue raisonné number or the edition details and lists that plate's past sales. This is shown alongside the price ladder; it is not an input to it.
3. **A calibrated ladder that also works without an estimate.** At auction, the ladder starts from the house estimate and corrects it by how prices have actually landed against estimates in that price band. For a dealer's or a platform's asking price, where there is no estimate, it starts from the nearest comparable sales of the same technique instead. The second case is where the tool differs most from reading the estimate; the example below shows the first case.

## 1. One lot, end to end

**Input.** Zao Wou-Ki, *Montagnes et soleil* (1951), lithograph, signed, numbered 192/200, catalogue raisonné Ågerup 59. Dobiaschofsky, Bern, sale of 6 November 2026. Estimate CHF 2,000–3,000 (about US$2,500–3,750).

**Output** (registered 1 November 2026, five days before the sale; key fields, USD):

```json
{
  "object_class": { "class": "signed_limited", "reasons": ["signed and numbered or edition stated"] },
  "plate": "zao_wou_ki:Agerup:59",
  "plate_basis": "catalogue_ref",
  "edition": { "edition_number": "192", "edition_size": 200, "signed": true },
  "same_plate_36m": { "n": 6, "median_usd": 3331, "last_date": "2026-05-19" },
  "mid": 3073,
  "mid_confidence": "high",
  "anchor_kind": "estimate",
  "anchor": 3125,
  "floor": 2500,
  "top": 4754,
  "band": 1.9,
  "confidence": "medium",
  "thresholds": { "suspect_below": 1250, "cheap_below": 2125 }
}
```

**How to read it.**

1. **Is it in scope?** The current calibration covers signed limited editions and proofs. This lot is signed and numbered, so it receives a range. Other kinds of object, such as reproductions, book pages and unsigned editions, receive no range for now, and the output says why. That is a limit of what has been calibrated, not a judgement about the object.
2. **Which plate, and how has it sold?** The catalogue number identifies the plate. It has 19 recorded auction sales since 2014. Six sales in the three years before registration had a median of US$3,331, against US$3,300–10,300 between 2014 and 2022. The latest sale, adjusted for the price level of the house where it sold, points to about US$3,073 (`mid`). These figures are context; they do not enter the floor or the ceiling.
3. **The ladder.** The anchor is the midpoint of the estimate, US$3,125. In this price band, past sales landed at or above 0.80 of the estimate midpoint about nine times in ten, so the floor is 0.80 × 3,125 = US$2,500. Here it happens to equal the low estimate; that is a coincidence of this lot, not a rule. The ceiling, US$4,754, is the upper end of the shortest range that has held 60% of past sales.
4. **When the two disagree.** If the same-plate figure sits far from the ladder, the plate has been selling differently from comparable prints. That is a reason to look at the plate's recent sales, not to move the ladder.
5. **Reading an asking price.** Below US$2,125 (0.85 × floor) the tool calls a price cheap. Below US$1,250 (0.5 × floor) it flags the price as unusually low and asks for a manual check of condition, attribution and the listing. These two multiples are design choices and have not been separately validated. The flag is a price anomaly signal only; the tool has no ability to judge authenticity.

**Price basis.** Sale prices include the buyer's premium wherever the source reports it. A minority of historical records only report the hammer price, and how to treat those is under review. Currencies are converted to US dollars at the Federal Reserve H.10 rate on the sale date, falling back up to 14 days for holidays. The tool does not adjust for condition, framing, or transaction costs; it places a price within the market for comparable sales and is not an appraisal of a single sheet.

Every output also carries a manifest: the protocol version, the parameters and a checksum for each input file, so each figure can be traced to the data snapshot it came from.

## 2. A live blind test

Twelve Zao Wou-Ki prints were offered at eight auction houses between 4 and 21 November 2026. The ladders were registered before any of them closed: floors and ceilings on 31 October (private repository commit `250f5fb`), plate identification and same-plate figures on 1 November (`6161b38`). The repository is private, so those commits cannot be inspected from outside; the public record on this page starts on 5 November 2026 (UTC), after the first lot (4 November) had closed and before the other eleven.

![Registered price ladders for twelve live lots](live-test-2026-11.svg)

| Closes | Lot | House | Estimate (USD) | Floor | Ceiling | Result |
| --- | --- | --- | --- | --- | --- | --- |
| 4 Nov | *La Cathédrale* 2/50 | Freeman's \| Hindman, New York | 4,000–6,000 | 3,531 | 8,255 | pending |
| 6 Nov | *Montagnes et soleil* Å.59, 192/200 | Dobiaschofsky, Bern | 2,500–3,750 | 2,500 | 4,754 | pending |
| 6 Nov | *Ohne Titel* Å.150, 82/125 | Dobiaschofsky, Bern | 2,500–3,750 | 2,500 | 4,754 | pending |
| 7 Nov | *Rivière* 189 (= Å.192), H.C. | Sturies, Düsseldorf | 3,510 | 2,808 | 5,340 | pending |
| 7 Nov | *Rivière* 220, *Canto Pisan* 45/50 | Sturies, Düsseldorf | 1,755 | 1,404 | 2,670 | pending |
| 7 Nov | *Rivière* 244, 78/95 | Sturies, Düsseldorf | 2,340 | 1,872 | 3,560 | pending |
| 7 Nov | *Rivière* 246, 75/95 | Sturies, Düsseldorf | 1,755 | 1,404 | 2,670 | pending |
| 9 Nov | Å.260, unsigned etching, ed. 125 | Alyes, Hong Kong (online) | 1,400–1,750 | not issued | not issued | pending |
| 10 Nov | *Sans titre* Å.192, 64/95 | Swann, New York | 3,500–4,500 | 2,825 | 6,604 | pending |
| 11 Nov | Untitled aquatint, 49/100 | DEWIT, Ostend | 4,680–5,850 | 3,718 | 8,693 | pending |
| 13 Nov | Å.328, ed. 99, foxing | Mainichi, Tokyo | 3,300–4,620 | 3,168 | 6,024 | pending |
| 21 Nov | *Composition* 38/125 | Schramm, Kiel | 1,123–1,404 | 1,264 | 2,543 | pending |

**What is being tested.** All twelve lots test the scope check: eleven were judged in scope and one, the unsigned etching at Alyes, out of scope. The eleven in scope test the price ladder.

**Scoring rules, fixed in advance.** A sold lot is scored on whether the price, including buyer's premium, is at or above the floor and whether it falls within the range. Unsold lots are reported as unsold and left out of the hold rate; withdrawn lots are reported and not scored. Results are taken from the auction house's or the platform's published result and added as each sale is reported. Nothing above the result column changes afterwards.

**What it can and cannot show.** Eleven lots show the process and record successes and failures honestly. They are too few to estimate accuracy; that comes from the historical tests below.

## 3. Historical testing against a simple baseline

The ladders were also tested on past sales, walking forward in time so that each prediction only used data available on its date. The baseline uses the auction house's own estimate as the ladder: low estimate as floor, high estimate as ceiling. Each cell reads *Kritis Print / baseline*.

| Period | Sales | Held at or above floor | Within the range | Range width (ceiling ÷ floor) |
| --- | --- | --- | --- | --- |
| Back-test 2015–2018 | 552 | 91.3% / 89.7% | 53% / 39% | 1.81 / 1.50 |
| Development 2019–2024 | 1,271 | 90.1% / 86.3% | 54% / 28% | 2.11 / 1.50 |
| Sealed 2025–2026, run once | 542 | 90.4% / 89.1% | 48% / 33% | 1.69 / 1.50 |

Zao Wou-Ki prints, estimate-anchored ladders. The floor holds 1 to 4 percentage points more often than the low estimate, and 15 to 26 percentage points more sales fall within the range. The range is also wider, so part of the gain in range hits may come from width alone. A comparison at equal width, or at equal coverage, has not been done yet and is the next test.

## Limits

- The method was developed on Zao Wou-Ki prints. Collection now covers more artists and houses, but the calibration has only been evaluated for a few of them.
- Historical results describe past data. They do not establish future accuracy or investment returns.
- The price reference places a price among comparable sales. It does not account for condition, framing or transaction costs, and it does not judge authenticity.

[Back to the project overview](../../projects/kritis-print.md)
