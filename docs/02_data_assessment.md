# Data Assessment

**Source:** AC2025_AnnualisedEntryExit_public.xlsx (TfL Annual Station Counts, crowding.data.tfl.gov.uk)
**Grain:** one row per station per mode (LU, London Overground, DLR, Elizabeth line)
**Header:** real column headers start at row 6 of the sheet (0-indexed row 5); rows above are titles/metadata

## Columns
Mode, MNLC, MASC, Station, Coverage, Source, then average entries/exits by day-of-week
(Monday, Midweek Tue-Thu, Friday, Saturday, Sunday), then Weekly / 12-week / Annualised totals.
Annualised = entries + exits combined already — do not re-sum Entry + Exit columns yourself.

## Known issues (found before any cleaning)
- 37 rows are cross-references to another mode's row (`---see LU/LO/EZL---`) — must exclude
  to avoid double-counting interchange stations.
- 11 rows use "Boarding/alighting" as the counting method instead of "Station entry/exit" —
  different measurement basis, excluded for consistency.
- 1 row (Cutty Sark DLR) is labeled `---station closed---` but has real non-zero figures —
  ambiguous, excluded pending clarification, not silently kept or dropped without a note.
- 5 stations have `---` (missing) values across the whole row despite normal labeling —
  no 2025 data collected, excluded from ranking rather than treated as zero.

## Cleaning rule
Keep only rows where Coverage == 'Station entry/exit' AND Annualised is numeric.
Result: 414 of 470 raw rows usable for analysis.
