# ODC-SCI-Public-Data
This data is used for the [ODC–SCI Dashboard](https://github.com/ATE-DRIVEN-lab/odc-sci-dashboard)

## public_data.csv


### Field Reference

| Field | Type | Format / Permitted values |
|-------|------|--------------------------|
| `ODCAccessionNbr` | numeric | unique assigned ID |
| `DOI` | string | full URL, e.g. `http://doi.org/10.7295/...` |
| `DatasetTitle` | string | free text |
| `DatasetTyp` | categorical | **lowercase**: `animal` · `animal - derived` · `cell` · `clinical` |
| `Year` | integer | **required** — rows with missing/non-numeric Year are dropped on load |
| `DatePublished` | string | `YYYY-MM-DD` |
| `Laboratory` | string | lab name |
| `StudyLeader` | string | name or `not reported` |
| `SubjectNbrs` | numeric | total unique subjects |
| `SpeciesTyp` | string | `rat` · `mouse` · `pig` · `monkey` · `human (deidentified)` — auto-converted to Title Case |
| `SpeciesStrainTyp` | string | free text or `not reported` |
| `SexTyp` | multi-value | `female` · `male` · `unknown` · `not reported` — **separate with `;`** |
| `AnimalSourceNam` | string | vendor/origin or `not reported` |
| `AgeVal` | string | free text, e.g. `75-83 days`, `8-12 weeks`, `18-89 years` |
| `BodyWgtMeasrVal` | string | free text in grams, e.g. `180-220 g` |
| `InjuryTyp` | multi-value | `contusion` · `neurologically intact` · `transection - hemisection` · `transection - DLQ` · `sham` — **separate with `;`** |
| `InjuryLevelAnatomical` | multi-value | **lowercase**: `cervical` · `thoracic` · `lumbar` — **separate with `;`** |
| `InjuryLevelSpinal` | string | e.g. `C5`, `T10`, `C1-L2` |
| `InjuryLaterality` | string | e.g. `unilateral`, `lateral`, `central` |
| `InjuryDevice` | multi-value | free text — **separate with `;`** |
| `InjurySeverity` | categorical | `mild` · `moderate` · `severe` · `incomplete` · `complete` · `AIS score A-E` · `not reported` |
| `InjuryContusionDataAvail` | multi-value | `force` · `programmed force` · `displacement` · `programmed displacement` · `velocity` · `programmed velocity` · `dwell time` · `programmed dwell time` — **separate with `;`** |
| `Locomotion` | multi-value | `BBB` · `BMS` · `ladder walking` — **separate with `;`** |
| `OtherBehaviour` | string | free text |
| `InterventionTyp` | multi-value | `drug/agent` · `electrical stimulation` · `diet` · `environmental` · `fecal microbiota transplant` · `genetic` · `graft/cellular` · `optogenetic` · `rehabilitative training` — **separate with `;`** |
| `InterventionAgent` | string | free text |
| `AuthorKeywords` | multi-value | free text — **separate with `;`**, auto-sorted alphabetically |
| `RelatedDatasets` | numeric | ODC accession number(s) of related datasets, or `NA` |
| `Funders` | multi-value | funder names — **separate with `;`**; grant numbers after `:` are stripped automatically (e.g. `NIH: R01NS123` → `NIH`) |
| `CoDES` | string | e.g. `pre`, `post` |
| `Purpose` | string | free text describing study purpose |
| `Notes` | string | free text or `NA` |

### Missing values

Any of the following are treated as missing and converted to `NA` internally:

```
na, n/a, not reported, not applicable, none, unknown, nan, (empty string)
```

### Exclusion rules

- Rows where **`Year`** is missing or non-numeric are automatically dropped.
- Rows with a non-empty **`retracted`** column (if that column exists) are excluded from display, but presented in the KPI datasets count.

---

## dict_data.csv

Each row describes one column from `public_data.csv`. Fixed column order:

```
VariableName, Title, Unit, Description, DataType, PermittedValues,
MinimumValue, MaximumValue, Comments
```

| Field | Rule |
|-------|------|
| `VariableName` | **exact** column name as it appears in `public_data.csv` |
| `Title` | human-readable label |
| `Unit` | unit of measurement, or `NA` |
| `Description` | full description; for categorical fields list permitted values in brackets: `[values: val1; val2]` |
| `DataType` | `numeric` · `string` · `categorical` · `ordinal`, or `NA` |
| `PermittedValues` | semicolon-separated list for categorical/ordinal fields; `NA` otherwise |
| `MinimumValue` | numeric lower bound, or `NA` |
| `MaximumValue` | numeric upper bound, or `NA` |
| `Comments` | additional notes, or `NA` |

---

