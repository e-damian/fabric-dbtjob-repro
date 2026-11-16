# fabric-dbtjob-repro

A minimal dbt project for reproducing Microsoft Fabric dbt job failures.
It has one model (`select 1 as id`) and no packages, so any failure comes
from how the job fetches or runs the project, not from the project itself.

Each scenario is a commit (and a tag) on top of the `baseline` tag.
