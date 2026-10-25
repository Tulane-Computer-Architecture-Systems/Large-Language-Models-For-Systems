# Data

This folder contains the per-study data of the survey as three UTF-8 encoded CSV files. Each file has one row per
work and a header row; the files share the join key `key`, the citation key of the work in the paper's bibliography.
Complete coding definitions, including the archetype and sub-group criteria, are given in
[`../method/coding-scheme.md`](../method/coding-scheme.md).

| File | Rows | Contents |
|---|---|---|
| [`corpus.csv`](corpus.csv) | 350 | Every included work: bibliographic identity and primary classification. |
| [`coding/archetype-studies.csv`](coding/archetype-studies.csv) | 317 | Additional coding of the archetype studies. |
| [`coding/benchmark-studies.csv`](coding/benchmark-studies.csv) | 33 | Additional coding of the benchmark and evaluation studies. |

## Empty Cells and Missing Information

Two conventions distinguish information that does not apply from information that is unavailable:

- **An empty cell** means that the field does not apply to the work, or, in the `doi` column only, that no DOI is
  available. An empty cell never denotes an uncoded value; every applicable field was coded for every work.
- **`not_reported`** means that the field applies but the paper does not provide the information needed to
  assign a value.

Values are interpreted by field. In reporting indicators such as `reports_time`, `no` means the corresponding
information is not reported; it does not mean that no cost was incurred. In mechanism fields, `no` or `none`
records the coded absence of the specified mechanism, while `not_reported`, where available, records insufficient
information. Counts of reported mechanisms exclude unknown values; non-reporting alone does not establish absence.

The table below lists every column that contains empty cells or `not_reported` values; all other columns are
complete for every row.

| File | Column | Empty cells | `not_reported` | Interpretation |
|---|---|---|---|---|
| `corpus.csv` | `doi` | 77 | – | No DOI is available, as for most machine-learning conference proceedings; the work is identified by `title`, `venue`, and `year`. |
| `corpus.csv` | `subgroup`, `inprocess_evaluation`, `trained_with_executable_reward`, `lm_runtime_presence` | 33 each | – | Benchmark and evaluation studies (`archetype` = `benchmark` or `evaluation`), which contribute no decision process of their own. |
| `corpus.csv` | `synthesis_mode` | 178 | – | All works other than C3 studies; the field applies to C3 only. |
| `coding/archetype-studies.csv` | `online_latency_reported` | 220 | – | Studies in which the model is not invoked online (`lm_runtime_presence` = `cached-artifact` or `absent`), for which inference latency does not affect operation. |
| `coding/archetype-studies.csv` | `model_access` | – | 5 | The paper does not identify the models used precisely enough to determine their access type. |
| `coding/archetype-studies.csv` | `human_approval` | – | 14 | The paper does not state whether a human approval or review step is part of the evaluated process. |
| `coding/benchmark-studies.csv` | `n_tasks` | – | 3 | The paper does not report the number of tasks. |

In `coding/benchmark-studies.csv`, the value `not-applicable` in `expert_reference` indicates that the study does not
measure performance, so no expert comparison is possible.

## `corpus.csv`

| Column | Definition |
|---|---|
| `key` | Citation key of the work in the paper's bibliography. |
| `name` | Short name of the system, benchmark, or study. |
| `title` | Title of the published version. |
| `venue` | Publication venue. |
| `year` | Year of publication. |
| `doi` | DOI of the published version. |
| `area` | Systems domain of the evaluated decision (ten areas). |
| `subarea` | Finer domain within the area. |
| `archetype` | `C1`–`C6` for archetype studies; `benchmark` or `evaluation` for the remaining works. |
| `subgroup` | Sub-group code and name within the archetype, for example `C3c feedback-guided refinement: validation feedback`. |
| `inprocess_evaluation` | The check within the proposed system that can change which candidate is accepted, refined, selected, or executed: `property-formal` (a property check, with or without a formal tool), `execution-reference` (execution against a reference implementation or testbench), `objective-measurement` (a measured value of the systems objective), `model-judge` (assessment by a language model), `human` (acceptance by a reviewer within the process), `mixed` (two classes decide jointly), or `none`. Checks used only as training rewards are not counted. |
| `study_evaluation` | The oracle the authors use to assess the system experimentally, with the same values as `inprocess_evaluation` plus `reference-match` (agreement with a reference output). |
| `synthesis_mode` | For C3 studies, the organization of candidate generation and selection: `single-pass`, `best-of-N`, `check-gated repair`, `measurement-driven repair`, `population search`, or `tree or beam search`. |
| `trained_with_executable_reward` | `yes` if model parameters are trained against a reward obtained by executing or checking candidates; otherwise `no`. |
| `lm_runtime_presence` | `online` (live inputs require model inference), `cached-artifact` (the model produces an artifact in advance that is later used without inference), or `absent` (the model influences only training or design). |

## `coding/archetype-studies.csv`

| Column | Definition |
|---|---|
| `key`, `name`, `archetype` | As in `corpus.csv`. |
| `model_access` | Access type of the models evaluated, by weight availability: `proprietary-api` (no evaluated model has public weights), `open-weights` (every evaluated model has public weights, however the study reached it), or `both`. |
| `adaptation` | Semicolon-separated adaptation mechanisms: `prompting`, `icl` (in-context examples), `rag` (retrieval), `memory` (external or accumulated memory), `sft` (supervised fine-tuning), `rl` (reinforcement learning), `preference` (preference optimization), `distillation`, and `other`. |
| `executor` | The actor that executes the consequential action on the target system: `machine`, `human`, or `no-consequential-action` when the evaluated process takes no action on a target system. |
| `human_approval` | `yes` if the evaluated process includes a human approval or review step, such as approving the model's output before use, reviewing it, or manually correcting or intervening on it; `no` for coded absence and `not_reported` when unspecified. The step need not precede an execution: studies in which nothing is executed on a target (`executor` = `no-consequential-action`) can also be `yes`. |
| `evidence_level` | The strongest setting in which the process is evaluated: `simulation`, `sandbox`, `benchmark-or-testbed`, `production-traces`, `human-reviewed-external-use`, `artifact-deployed`, or `component-deployed`. |
| `coordination` | `single-role` (one model role), `multi-role` (distinct functions assigned to two or more model roles), or `replicated-role` (the same role replicated across parallel workers, nodes, or components). |
| `model_critic` | `yes` if one model role reviews or judges the output of another. |
| `backbone_comparison` | `yes` if results are reported for more than one backbone model under otherwise controlled conditions; `no` otherwise. This field does not count every study that names or evaluates multiple models. |
| `online_latency_reported` | For online-inference studies, `yes` if inference latency is reported and `no` otherwise; blank for studies without online inference. |
| `reports_time` | `yes` if the inference cost of the method is reported as wall-clock time. |
| `reports_tokens` | `yes` if the inference cost is reported as token counts. |
| `reports_monetary_cost` | `yes` if the inference cost is reported as monetary cost. |
| `reports_training_compute` | `yes` if training or other offline compute is reported. |

## `coding/benchmark-studies.csv`

Unless stated otherwise, columns take the values `yes` or `no`.

| Column | Definition |
|---|---|
| `key`, `name` | As in `corpus.csv`. |
| `study_role` | `benchmark` (a reusable task suite) or `evaluation` (an evaluation of existing models or systems). |
| `environment` | `static` (fixed inputs) or `interactive` (the evaluated system acts on an environment that responds). |
| `action_rights` | The action authority of the evaluated system, in the paper's terms: the actions the harness permits it to take, `propose-only` or `execute-in-sandbox`. |
| `n_tasks` | Number of tasks in the suite. |
| `feedback_to_system` | Whether the harness returns feedback to the evaluated system; `secondary-variant-only` if only a secondary configuration does so. |
| `measures_performance` | Whether a systems performance objective is measured in addition to functional correctness. |
| `expert_reference` | Whether measured performance is compared with an expert or state-of-practice reference; `not-applicable` if performance is not measured. |
| `repeated_evaluation` | Whether each task is evaluated more than once. |
| `contamination_control` | Whether training-data contamination is measured or tested. |
| `reports_inference_cost` | Whether the inference cost of the evaluated models is reported. |
| `operates_running_target` | Whether the evaluated system must operate a running target system. |
