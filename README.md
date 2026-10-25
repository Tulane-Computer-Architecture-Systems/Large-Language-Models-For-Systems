# Supplementary Material: Large Language Models for Systems Optimization, Management, and Control

This repository contains the supplementary material of the survey. It documents the search and selection
procedure, the classification applied to each included work, and the per-study coding from which the counts reported
in the paper are derived.

## Corpus

The survey includes 350 works: 317 archetype studies, which propose and evaluate a decision
process in which a language model participates, and 33 benchmark or evaluation studies. The archetype studies
are distributed across the six archetypes as follows: C1 25, C2 26, C3 172,
C4 33, C5 27, and C6 34.

## Contents

| Path | Contents |
|---|---|
| [`data/README.md`](data/README.md) | Description of the data files, their columns, and the interpretation of empty cells and `not_reported` values. |
| [`data/corpus.csv`](data/corpus.csv) | One row per included work: bibliographic identity (title, venue, year, DOI), systems area, and primary classification (archetype, sub-group, in-process and study evaluation, synthesis mode, run-time presence of the model). |
| [`data/coding/archetype-studies.csv`](data/coding/archetype-studies.csv) | Coding of the 317 archetype studies: model access, adaptation, execution authority, human approval, evidence level, coordination, and cost reporting. |
| [`data/coding/benchmark-studies.csv`](data/coding/benchmark-studies.csv) | Coding of the 33 benchmark and evaluation studies: environment, action authority, task count, and evaluation properties. |
| [`method/`](method/) | Search specification, eligibility criteria, and coding scheme; [`method/README.md`](method/README.md) describes the folder. |
| [`tables/archetype-membership.md`](tables/archetype-membership.md) | Full references for every included work, grouped by archetype and sub-group. |
| [`tables/representative-systems.md`](tables/representative-systems.md) | 48 representative systems with their reported results and reference points. |
| [`tables/benchmark-suites.md`](tables/benchmark-suites.md) | The 33 benchmark and evaluation studies: task artifact, environment, action authority, task count, oracle, and reference point, followed by the aggregate property counts. |
| [`tables/deployment-evidence.md`](tables/deployment-evidence.md) | The 44 archetype studies whose evidence extends beyond benchmarks, simulation, or sandboxes: what ran, who acts, scale or duration, and what was measured. |

All data files are UTF-8 encoded CSV and share the join key `key`, the citation key of each work in the paper's
bibliography. Column definitions and the treatment of empty cells are given in [`data/README.md`](data/README.md). Paper full texts
are not redistributed; each work is identified by its DOI, or, for the 77 works without an available DOI, by its
venue and year.

## License
CC-BY 4.0 license applies to the data files and tables in this repository.

## Citation
If you use this material, please cite the accompanying survey, "Large Language Models for Systems Optimization,
Management, and Control", submitted to the Journal of Systems Architecture. Full citation details will be added when
the paper is published.
