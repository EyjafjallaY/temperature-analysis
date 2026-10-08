# Data

## Source and coverage

`data.csv` is the dataset distributed with [MIT OCW 6.0002, Fall 2016, Problem Set 5](https://ocw.mit.edu/courses/6-0002-introduction-to-computational-thinking-and-data-science-fall-2016/resources/ps5/). The project dataset was compared with the official archive and is byte-for-byte identical. It is included unchanged under the upstream sharing terms described in [provenance](provenance.md).

- 421,848 records, 21 cities.
- Dates: 1961-01-01 through 2015-12-31.
- 1,155 city-year groups, each with a complete 365- or 366-day calendar.
- No missing values or duplicate city-date keys in the supplied file.
- Temperature is modeled in degrees Celsius.

| Column | Meaning | Format |
| --- | --- | --- |
| CITY | City identifier | Text |
| TEMP | Recorded daily temperature | Number |
| DATE | Calendar date | YYYYMMDD |

The header order is `CITY,TEMP,DATE`. The project uses the dataset as distributed; it does not independently establish its measurement-station provenance or whether each daily record was originally computed as a mean, minimum or maximum.

## Integrity

The SHA-256 of both the local and official CSV is:

```text
7f58135c2dd7b7fbbd96e0d61490dc7b5d2d7d5c5205d72897839afbb06a8e4c
```

To obtain the file independently, download the official PS5 archive from the resource page and extract only `data.csv` into the project root. Keep the raw values unchanged when reproducing the original results.

## Known data issue

The distributed CSV contains the record `PHOENIX, -483.3, 19640914`. This implausible temperature is present in the official archive too. It is retained to preserve the original input and experiment. No corrected or filtered analysis is presented here, and its effect has not been quantified through a separate cleaning experiment.

Users performing a new analysis should specify a justified quality-control policy, keep the original input, and recompute metrics after any change. Such a result would be a new experiment rather than a reproduction of this one.

## Aggregation and evaluation

City annual means are averaged with equal city weights. The predictor is calendar year. Training covers 1961–2009; testing covers 2010–2015. The moving average uses up to five observations and resets at each segment's start. The prediction target is the smoothed cohort annual mean, not daily temperature. Full definitions are in [analysis](analysis.md).
