# fabric-dbtjob-repro

A minimal dbt project for reproducing two Microsoft Fabric dbt job failures.
It has one model (`select 1 as id`) and no packages, so any failure comes
from how the job fetches the project, not from the project itself.

## Branches to point a dbt job at

| Branch | Content | Result |
|---|---|---|
| `pass` | baseline project only | succeeds |
| `fail` | baseline plus one unused file with a 147-character relative path | fails: "Failed to download dbt project from GitHub repository" |

Both names are four characters, like `main`, so the extraction folder name
has the same length in every run.

## Tags (one per scenario)

Each scenario is the baseline plus at most one unused file under `longpath/`.
No folder or file name is longer than 50 characters.

| Tag | Relative path of the extra file | Result |
|---|---|---|
| `baseline` | none | pass |
| `scenario-rel94` | 94 | pass |
| `scenario-rel95` | 95 | pass |
| `scenario-rel120` | 120 | not run |
| `scenario-259` | 145 | fail |
| `scenario-260` | 146 | fail |
| `scenario-261` | 147 | fail |
| `scenario-baseline-again` | none (same tree as `baseline`) | pass |
| `scenario-target-path` | none; adds a model whose `not_null` test compiles to a 306-character path | pass with `dbt build` |
