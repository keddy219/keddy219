# Kritis

Kritis is a Python research tool for analysing comparable auction sales and producing market-positioning reports for unique artworks. Its initial work focuses on paintings by Zao Wou-Ki.

## The problem

An auction price depends on the work being sold and the conditions of the sale. A useful research report needs to explain which records are comparable, how they inform the result, and where the evidence is limited.

Kritis takes artwork information as input and produces a report with comparable sales, valuation calculations, reference intervals, and limitations. It includes workflows with and without an auction estimate, and can withhold a result when required information is missing.

## Development approach

The project keeps versioned data snapshots, model artifacts, and evaluation records. This supports tracing a reported result to its data and method.

I lead the research requirements and domain rules, use AI-assisted development for implementation, and review whether the outputs meet the intended use.

## Current stage

Kritis remains a research system. Its full precision criteria have not been met. Existing historical evaluations must be read with their documented data-exposure and evaluation limits; they do not establish a successful blind prospective test.

The source code and underlying datasets are currently private.

