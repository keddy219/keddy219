# Kritis Print

Kritis Print is a Python research tool for analysing the market for editioned prints. It first decides which print sales are worth comparing, then combines auction-estimate calibration with same-plate sales data to give a traceable market price reference.

## The problem

Auction records can mix signed limited editions, proofs, reproductions, and pages from books or magazines. These distinctions affect which sales are useful comparisons.

Kritis Print classifies the object before issuing a price range. For eligible prints, it calculates a reference range and can assess a supplied price against that range. It also adds same-plate sales information when available.

## Method and output

The range uses an auction estimate or a comparable-sales anchor, calibrated against recent sale-to-anchor ratios grouped by price band. Same-plate comparisons are presented separately. Outputs include the object class, the price range, the basis for the calculation, and reasons for withholding a result when information is insufficient.

The project also includes data-collection workflows and liquidity reports.

## Current stage

The tool is implemented and remains under evaluation. The initial pricing method has been developed around prints by Zao Wou-Ki; data collection is expanding to other artists. Its price ranges are research references. Historical coverage results do not establish prospective accuracy or investment returns.

The source code and underlying datasets are currently private.

**See it in action:** [example output](../examples/kritis-print/README.md). A short animation and one real lot from input to price range, plus a live test of twelve lots recorded before their sales.

