# Coding Scheme

This document defines the classification applied to every included work and the fields of the released data files.
The coding records information extracted from the included works. A blank cell denotes a field that does not apply
(for example, archetype fields for benchmark studies), except that a blank DOI denotes an unavailable identifier.
`not_reported`, where available, records insufficient information. Reporting indicators use `no` when the specified
information is not reported; this does not imply that no cost was incurred. Mechanism fields use `no` or `none`
for the coded absence of the specified mechanism. Counts of reported mechanisms exclude unknowns; non-reporting
alone does not establish that a mechanism is absent. See [`../data/README.md`](../data/README.md) for field-specific
missing-value conventions.

## 1. Unit of Analysis and Study Role

The unit of analysis is the *evaluated process*: the decision process whose behavior the study measures. Each work
receives one study role. An *archetype study* (317 works) proposes and evaluates a decision process in which a
language model participates. A *benchmark* or *evaluation study* (33 works) evaluates models or systems on a
task suite without contributing a decision process of its own. Where a study describes materially different
training-time and operating-time processes, the archetype is assigned from the process central to its evaluated
contribution.

## 2. Archetype and Sub-group

Each archetype study is assigned one primary archetype, determined by the model's contribution, the evaluation applied
to candidates, and the allocation of selection and execution authority (Section 4 of the paper). Each archetype is
partitioned into sub-groups by a single structural criterion: where the model output enters the conventional decision
function (C1); what the model supplies to the optimizer (C2); how candidate evaluation and selection are organized
(C3); the basis of property checking (C4); what mediates between the model's diagnosis and the operator (C5); and what
the model emits as the executed output (C6). Counts are given in parentheses.

| Code | Archetype | Sub-groups |
|---|---|---|
| C1 | Auxiliary intelligence for conventional control | C1a input augmentation (11); C1b objective translation (8); C1c policy shaping (6) |
| C2 | Model-guided optimization and search | C2a search-space shaping (13); C2b candidate-point proposal (11); C2c move-level guidance (2) |
| C3 | Candidate synthesis | C3a single-pass synthesis (56); C3b best-of-N selection (12); C3c feedback-guided refinement: validation feedback (33); C3d feedback-guided refinement: quantitative feedback (45); C3e search-based synthesis (26) |
| C4 | Property-checked synthesis | C4a formal equivalence (9); C4b execution-based conformance (3); C4c proof-obligation checking (3); C4d side-condition checking (18) |
| C5 | Advisory diagnosis and management | C5a direct advisory (7); C5b model-mediated adjudication (18); C5c symbolic validation (2) |
| C6 | Operational actuation | C6a policy value (16); C6b event-triggered decision (3); C6c tool-call sequence (8); C6d deployed artifact (7) |

Archetype assignment follows the evaluated process and its governing acceptance criterion, rather than the presence
of a checker alone. C4 centers on property-checked acceptance; C3 centers on candidate synthesis with reference
execution, measurement, refinement, or search. C3 processes can also contain property checks, and checks at different
stages may serve different purposes. The `inprocess_evaluation` field records the coded check separately from the
primary archetype. C5 and C6 distinguish advisory output from machine-executed actuation: C5 does not itself perform
state-changing operations on the operated system; C6 passes model output to machine execution, sometimes subject
to human approval. Some C5 studies evaluate recommendations or downstream artifacts without acting on an operated
system.

## 3. Field Definitions: `data/corpus.csv`

| Field | Definition and values |
|---|---|
| `key` | Citation key of the work in the paper's bibliography; the join key for all data files. |
| `name` | Short name of the system, benchmark, or study. |
| `title`, `venue`, `year`, `doi` | Bibliographic identity of the published version. `doi` is blank where no DOI is available. |
| `area`, `subarea` | Systems domain of the evaluated decision (ten areas, 49 subareas). |
| `archetype` | `C1`–`C6` for archetype studies; `benchmark` or `evaluation` for the remaining works. |
| `subgroup` | Sub-group code and name (Section 2). |
| `inprocess_evaluation` | The check that can change which candidate is accepted, refined, selected, or executed during the evaluated process: `property-formal` (a property check, with or without a formal tool), `execution-reference` (execution against a reference implementation or testbench), `objective-measurement` (a measured value of the systems objective), `model-judge` (assessment by a language model), `human` (acceptance by a reviewer inside the process), `mixed` (two classes jointly decide), or `none`. Checks used only as training rewards are excluded. |
| `study_evaluation` | The oracle the authors use to assess the system experimentally, with the same values plus `reference-match` (agreement with a reference output). |
| `synthesis_mode` | C3 only: `single-pass`, `best-of-N`, `check-gated repair`, `measurement-driven repair`, `population search`, or `tree or beam search`. |
| `trained_with_executable_reward` | `yes` if model parameters are trained against a reward obtained by executing or checking candidates. |
| `lm_runtime_presence` | `online` (live inputs require model inference), `cached-artifact` (the model produces an artifact in advance that is later used without inference), or `absent` (the model influences only training or design). |

## 4. Field Definitions: `data/coding/archetype-studies.csv`

One row per archetype study.

| Field | Definition and values |
|---|---|
| `model_access` | By weight availability of the models evaluated: `proprietary-api` (no evaluated model has public weights), `open-weights` (every evaluated model has public weights, however the study reached it), or `both`. |
| `adaptation` | Semicolon-separated adaptation mechanisms: `prompting`, `icl` (in-context examples), `rag` (retrieval), `memory` (external or accumulated memory), `sft` (supervised fine-tuning), `rl` (reinforcement learning), `preference` (preference optimization), `distillation`, and `other`. |
| `executor` | Who executes the consequential action on the target system: `machine`, `human`, or `no-consequential-action` when the evaluated process takes no action on a target system. |
| `human_approval` | `yes` if the evaluated process includes a human approval or review step, such as approving the model's output before use, reviewing it, or manually correcting or intervening on it. The step need not precede an execution: studies in which nothing is executed on a target (`executor` = `no-consequential-action`) can also be `yes`. |
| `evidence_level` | Strongest setting in which the process is evaluated: `simulation`, `sandbox`, `benchmark-or-testbed`, `production-traces`, `human-reviewed-external-use`, `artifact-deployed`, or `component-deployed`. |
| `coordination` | `single-role` (one model role), `multi-role` (distinct functions assigned to two or more model roles), or `replicated-role` (the same role replicated across parallel workers, nodes, or components). |
| `model_critic` | `yes` if one model role reviews or judges the output of another. |
| `backbone_comparison` | `yes` if results are reported for more than one backbone model under otherwise controlled conditions; `no` otherwise. This field does not count every study that names or evaluates multiple models. |
| `online_latency_reported` | For online-inference studies, `yes` if inference latency is reported and `no` otherwise; blank for studies without online inference. |
| `reports_time`, `reports_tokens`, `reports_monetary_cost` | `yes` if the paper reports the inference cost of its method in wall-clock time, token counts, or monetary cost, respectively. |
| `reports_training_compute` | `yes` if the paper reports training or other offline compute. |

## 5. Field Definitions: `data/coding/benchmark-studies.csv`

One row per benchmark or evaluation study. Unless stated otherwise, fields take the values `yes`, `no`, or
`not-applicable`.

| Field | Definition and values |
|---|---|
| `study_role` | `benchmark` (a reusable task suite) or `evaluation` (an evaluation of existing models or systems). |
| `environment` | `static` (fixed inputs) or `interactive` (the evaluated system acts on an environment that responds). |
| `action_rights` | Action authority: `propose-only` or `execute-in-sandbox`. |
| `n_tasks` | Number of tasks in the suite, where reported. |
| `feedback_to_system` | Whether the harness returns feedback to the evaluated system; `secondary-variant-only` if only a secondary configuration does so. |
| `measures_performance` | Whether a systems performance objective is measured, beyond functional correctness. |
| `expert_reference` | Whether performance is compared with an expert or state-of-practice reference; `not-applicable` if performance is not measured. |
| `repeated_evaluation` | Whether each task is evaluated more than once. |
| `contamination_control` | Whether training-data contamination is measured or tested. |
| `reports_inference_cost` | Whether the inference cost of the evaluated models is reported. |
| `operates_running_target` | Whether the evaluated system must operate a running target system. |

## 6. Synthesis Modes and Run-Time Presence in the Corpus

Among the 172 C3 studies, 56 use single-pass synthesis, 12
best-of-N selection, 33 check-gated repair, 45
measurement-driven repair, 14 population search, and 12 tree or
beam search; 22 of them additionally train against an executed reward. Across the
317 archetype studies, the model is present online in 97, as a cached artifact in
206, and absent at run time in 14.
