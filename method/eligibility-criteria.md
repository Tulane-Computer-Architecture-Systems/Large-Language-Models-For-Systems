# Eligibility Criteria

Each work retained after title and abstract screening was assessed against the five criteria below. A work was
included only if it satisfied all five. Criteria that could not be resolved from the abstract, typically P4 and P5,
were resolved during full-text review. The criteria were applied before the venue criterion and the scope
clarifications described in Section 3 of the paper.

| Criterion | Requirement | Grounds for exclusion |
|---|---|---|
| **P1** | Uses a general-purpose pretrained generative language model | Uses only encoder, forecasting, or small domain models trained from scratch |
| **P2** | Model output contributes to a systems or hardware decision | The model only predicts, classifies, detects, summarizes, or answers questions, or is itself the workload being served or trained |
| **P3** | Targets a systems or hardware property | No systems objective is evaluated, such as performance, cost, reliability, utilization, or artifact correctness |
| **P4** | Evaluates the model contribution in an implemented workflow | Survey, position paper, plan-only demonstration, or model contribution that cannot be evaluated separately |
| **P5** | Evaluation reaches an external outcome | Evaluation stops at text similarity or model judgment, without measurement, a toolchain oracle, or an operational decision |

## Scope Clarifications

The following clarifications were adopted during full-text review and applied uniformly to all works retained at that
stage. The criterion on which each rests is given in parentheses.

- **Self-contained code-optimization exercises** are excluded (P3). Studies remain eligible when optimization targets
  a real software system, workload, or hardware platform.
- **Label-only diagnosis** is excluded (P2, P5). Diagnostic studies remain eligible when the diagnosis informs an
  operational decision and is evaluated against an external outcome (P5).
- **Software testing and bug finding** are excluded as primary objectives (P3). Testing remains eligible when it
  serves as an oracle for a generated design, kernel, or configuration.
- **Small, from-scratch, and encoder-style models** are excluded (P1). The review is limited to general-purpose
  pretrained generative language models. One LLM-scale study is retained: Cummins et al. (2023) train the Llama 2 7B
  architecture and tokenizer without pretrained weights, as the precursor of LLM Compiler, which continues pretraining
  Code Llama for the same task.
- **Studies with insufficient evidence** are excluded (P4). The paper must establish both the model's role and its
  evaluated contribution.
- **Security** analysis, vulnerability discovery, exploit generation, and security testing are excluded as a distinct
  adjacent literature. Security mechanisms remain in scope when they constrain a systems optimization, management, or
  control decision.
