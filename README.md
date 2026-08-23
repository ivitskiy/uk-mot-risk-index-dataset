# MOT Risk Index Evidence Capsule — 2024 v2

This package is a machine-readable release of aggregated MOT inspection outcomes for 34 vehicle families in Great Britain. It contains family-level initial-test outcomes and a separate family-by-defect-group table that shows where failure items are over-represented against the national class-4 benchmark. The canonical dataset page is [UK MOT failure rates 2024](https://motriskindex.co.uk/statistics/mot-failure-rates/).

## Files

- `motriskindex-families-2024-v2.csv` — one row per published vehicle family.
- `motriskindex-defect-groups-2024-v2.csv` — one row per published family and prespecified top-level defect group.
- `manifest.json` — release metadata and a source, licence, unit, denominator and one-sentence definition for every CSV column.
- `CITATION.cff` — citation metadata for repositories and research catalogues.
- `checksums.txt` — SHA-256 digests for every payload and metadata file in the package.

Every CSV row has a stable `claim_id`. No vehicle-level records, registration marks or geographic slices are included.

## How it was assembled

The source is the DVSA Anonymised MOT tests and results bulk dataset for calendar 2024. The family denominator includes first-time class-4 examinations (`test_type=NT`) with outcomes P, F or PRS; retest records are excluded from these rates. PRS means a failing defect was found during the initial examination and rectified at the test station, so the initial-failure numerator is F + PRS; the strict-fail column counts F only.

The headline metric is the **age-adjusted MOT initial-failure ratio**. For each family, observed F + PRS initial failures are divided by the expected count obtained by applying frozen national initial-failure rates to that family's tests in the following age strata: under 3 years, each single year from 3 through 19, 20 years and over, and unknown. The result is multiplied by 100, so 100 is the outcome expected for that age profile. The interval columns are 95% Wilson-score intervals on the observed initial-failure proportion, scaled by the same frozen expected count.

Defect-group rates count F or M coded failure-item occurrences, not distinct vehicles and not the percentage of tests with any item in that group. A test can contain more than one failure item. `failure_items_per_100_tests` uses the family's eligible initial tests as its denominator; `excess_pp` subtracts the national rate for the same group, and `over_representation_ratio` divides by that national rate.

Families or defect-group cells with `n < 1,000` are omitted completely. Published rows with `n` from 1,000 through 5,000 inclusive have `confidence=low_sample`. When exactly one cell in a complete family defect-group slice is suppressed, the next-smallest cell is also omitted so the first cannot be reconstructed by subtraction.

## Scope and limitations

These are observational inspection outcomes, not causal estimates. Mileage is not adjusted or aligned between families, and differences may also reflect fleet use, fuel mix, maintenance, test presentation and other residual confounding. MOT inspections do not observe all mechanical or electronic systems, so the data do not measure breakdowns, owner complaints or the condition of an individual vehicle.

The release covers Great Britain, not Northern Ireland, and calendar 2024 only. Make and model values in the source are free text; the family mapping is explicit and conservative. See `manifest.json` for the exact grain and denominator of each column.

## Licence and attribution

Source data is Crown copyright and was supplied by the Driver and Vehicle Standards Agency. It is used under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/). Contains public sector information licensed under the Open Government Licence v3.0.

Original MOT Risk Index derivations and metadata in this package are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Suggested attribution: “MOT Risk Index Research Desk, MOT Risk Index Evidence Capsule — 2024 v2, https://motriskindex.co.uk/statistics/mot-failure-rates/”. The underlying DVSA material remains under the Open Government Licence v3.0.

Questions and corrections: [data@motriskindex.co.uk](mailto:data@motriskindex.co.uk).
