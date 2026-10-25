# Benchmark and Evaluation Studies

The 33 benchmark and evaluation studies of the corpus, grouped by what the evaluated system is asked to
produce. A *benchmark* is a reusable task suite; an *evaluation study* assesses existing models or systems without
contributing a reusable suite. These studies are analyzed by evaluation task and harness rather than assigned a
decision-process archetype.

Columns record what the evaluated system produces (task artifact), whether inputs are fixed or the system acts on a
responding environment (environment), what the harness permits it to do (action authority), the number of distinct
tasks as reported, the oracle applied to its output, and the reference point against which performance or
correctness is judged. An em dash in the last column indicates that the study applies no reference beyond its own
oracle. Rows summarize the evaluation configurations reported in the cited studies; some studies also evaluate
secondary configurations with different interaction or feedback arrangements.

The same studies are coded field by field in
[`../data/coding/benchmark-studies.csv`](../data/coding/benchmark-studies.csv), and their bibliographic records are
in [`../data/corpus.csv`](../data/corpus.csv).

| Study | Role | Task artifact | Environment | Action authority | Tasks | Oracle | Reference point |
|---|---|---|---|---|---|---|---|
| **Hardware design and verification** | | | | | | | |
| FVEval [1] | benchmark | SVA from text or RTL | static | propose only | 571 | Jasper syntax; formal equivalence with reference; proof on design (vacuous accepted) | Reference assertion |
| Assertion-generation study [2] | evaluation | SVA from RTL | static | propose only | 100 | JasperGold proof (vacuous counted as pass) | — |
| Multimodal Verilog benchmark [3] | benchmark | Verilog from diagrams and text | static | propose only | ≈32 | Testbench simulation, best of 5 | — |
| RTL generation review [4] | evaluation | Verilog from specification | interactive | sandbox | 207 | Benchmark testbenches (Icarus) | — |
| FIXME [5] | benchmark | Verification artifacts and fixes | interactive | propose only | 180 | VCS simulation; answer key; embedding similarity | — |
| Bench4HLS [6] | benchmark | HLS C++ with pragmas | static | propose only | 170 | Simulation, synthesis, implementation; PPA | Reference design |
| PICBench [7] | benchmark | Photonic circuit netlist | interactive | propose only | 24 | Simulated response vs. golden design | Golden design |
| Rule2DRC [8] | benchmark | DRC script from rule text | interactive | sandbox | 1,000 | Violations match ground-truth script on all layouts | Ground-truth script |
| VerilogEval [9] | benchmark | Verilog module from a text description | static | propose only | 156 | Transient simulation against a golden solution; pass@k | Golden reference solution |
| OpenLLM-RTL [10] | benchmark | Verilog RTL from a description; SVA from a specification | static | propose only | 50 | Syntax and functional simulation; formal property verification | Reference design |
| **Kernels and parallel code** | | | | | | | |
| ParEval [11] | benchmark | Parallel function bodies | static | propose only | 420 | Output vs. sequential code; speedup, efficiency | Sequential code |
| PCEBench [12] | benchmark | OpenMP/MPI code | static | propose only | 621 | Tests, race detection, speedup threshold | Sequential code |
| Zero-shot parallelization study [13] | evaluation | OpenMP version of kernel | static | propose only | 30 | Memory/thread checks, output diff, speedup | Intel compiler auto-parallelization |
| KernelBench [14] | benchmark | CUDA kernels for PyTorch models | static | propose only | 250 | Five random inputs; timing (fastp) | PyTorch eager, torch.compile |
| KernelCraft [15] | benchmark | Assembly kernels, new ISAs | interactive | sandbox | 33 | Allclose vs. reference; cycles or latency | Platform compiler; expert (one platform) |
| CUDAnalyst [16] | evaluation | Plans and kernel rewrites | interactive | propose only | not reported | Compile, pass, faster than baseline | Baseline kernel |
| **Program and repository performance** | | | | | | | |
| AlgoTune [17] | benchmark | Faster Python solver | interactive | sandbox | 154 | Verifier on held-out inputs; speedup (floor 1×) | Reference solver |
| SWE-fficiency [18] | benchmark | Repository patch | interactive | sandbox | 498 | Covering unit tests; speedup ratio | Expert patch |
| SWE-Perf [19] | benchmark | Repository patch | interactive | sandbox | 140 | Performance-related tests; significant runtime gain | Expert patch |
| Energy-of-optimization study [20] | evaluation | Optimized Python function | interactive | propose only | 118 | Tests; CPU instructions; energy | Reference solutions |
| Assistant-written code study [21] | evaluation | C++ written with an assistant | interactive | propose only | 2 | Sanity checks; runtime over 32 runs | Unaided developers; expert solutions |
| Web-performance study [22] | evaluation | Edited HTML | static | propose only | 15 | Lighthouse audit incidence; no functional check | Original page |
| **Configuration, specification and infrastructure** | | | | | | | |
| IaC-Eval [23] | benchmark | Terraform program | static | propose only | 458 | `terraform plan`; intent policy | — |
| KGen [24] | evaluation | Kubernetes manifest from generated intent | static | propose only | not reported | YAML parse; kubectl validation; similarity to original | Original manifest |
| NetConfEval [25] | benchmark | Specifications, calls, code, router configurations | static | propose only | not reported | Exact match; tests; load and text similarity | — |
| OSVBench [26] | benchmark | Kernel syscall specification | static | propose only | 245 | Verifier verdicts equal the oracle's | Oracle specification |
| Index-tuning study [27] | evaluation | Index configuration | static | propose only | 127 | Measured execution time | SQL Server tuning advisor |
| **Operations and control** | | | | | | | |
| ITBench [28] | benchmark | Diagnoses, mitigations, policies | interactive | sandbox | 94 | Root-cause label; alert cleared; cost | — |
| DevOps-Gym [29] | benchmark | Builds, diagnoses, patches, tests | interactive | sandbox | 726 | Builds and tests; anomaly-type label | — |
| AIOpsLab [30] | benchmark | Detection, localization, root cause, executed mitigation | interactive | sandbox | 48 | Injected-fault labels; whole-system health after the actions | Classical AIOps detectors |
| R2Act [31] | benchmark | Typed recovery plan (operation, target, required fields) | static | propose only | 302 | Membership in the annotated valid-plan set; live replay health check | Annotated valid plans |
| HPC scheduling study [32] | evaluation | Scheduling action per event (start, backfill, delay, stop) | interactive | sandbox | 43 | Simulated makespan, wait, utilization, fairness | FCFS, SJF; OR-Tools solver |
| Autoscaling study [33] | evaluation | Autoscaler manifests; replica counts | interactive | sandbox | 6 | Latency, success rate, efficiency under load | HPA; expert-tuned KEDA |

## Aggregate Properties

Counts of the same 33 studies by study role: *B* benchmarks, *E* evaluation studies. Every count is derived
from [`../data/coding/benchmark-studies.csv`](../data/coding/benchmark-studies.csv) and the corpus coding.
The per-study rows and aggregate counts use the same coding records. The four oracle categories are exclusive and partition
the 33 studies; the other properties are independent and do not sum to the total.

*Feedback to evaluated system* counts a study whose harness returns any feedback to the system under evaluation,
including the 7 studies that do so only in a secondary variant (coded `secondary-variant-only` in the
released data). No benchmark or evaluation harness among these 33 studies grants the evaluated system
authority over production infrastructure.

| Property | B | E | All |
|---|---|---|---|
| **Studies** | **22** | **11** | **33** |
| **Interaction and authority** | | | |
| Interactive environment | 10 | 6 | 16 |
| Sandboxed actuation | 8 | 3 | 11 |
| Running target required | 3 | 1 | 4 |
| Feedback to evaluated system | 15 | 5 | 20 |
| Production authority | 0 | 0 | 0 |
| **Study-evaluation oracle** | | | |
| Property or formal check | 3 | 1 | 4 |
| Reference execution | 4 | 1 | 5 |
| Measurement only | 0 | 4 | 4 |
| Multiple oracle classes | 15 | 5 | 20 |
| **Reporting and evaluation design** | | | |
| Performance measured | 8 | 8 | 16 |
| Expert or state-of-practice reference | 6 | 6 | 12 |
| Repeated trials | 17 | 8 | 25 |
| Contamination tested or mitigated | 7 | 1 | 8 |
| Inference cost reported | 7 | 5 | 12 |

## References

1. Kang, M., Liu, M., Hamad, G. B., Suhaib, S. M., and Ren, H. (2025). FVEval: Understanding Language Model Capabilities in Formal Verification of Digital Hardware. *2025 Design, Automation & Test in Europe Conference (DATE)*, 1–6. https://doi.org/10.23919/date64628.2025.10992720
2. Pulavarthi, V., Nandal, D., Dan, S., and Pal, D. (2025). Are LLMs Ready for Practical Adoption for Assertion Generation?. *2025 Design, Automation & Test in Europe Conference (DATE)*, 1–7. https://doi.org/10.23919/date64628.2025.10992817
3. Chang, K., Chen, Z., Zhou, Y., Zhu, W., Wang, K., Xu, H., et al. (2024). Natural language is not enough: Benchmarking multi-modal generative AI for Verilog generation. *Proceedings of the 43rd IEEE/ACM International Conference on Computer-Aided Design*, 1–9. https://doi.org/10.1145/3676536.3676679
4. Ravindran, A., Patra, A., Babaey, V., and Purini, S. (2026). A Critical Review and Evaluation of LLMs for RTL Generation. *IEEE Access*, 14, 28522–28539. https://doi.org/10.1109/access.2026.3665894
5. Wan, G., Wong, S., Su, S., Niu, C., Wang, N., Wan, X., et al. (2026). FIXME: Towards End-to-End Benchmarking of LLM-Aided Design Verification. *Proceedings of the AAAI Conference on Artificial Intelligence*, 40(2), 1087–1095. https://doi.org/10.1609/aaai.v40i2.37079
6. Khan, M. Z. S., Azar, K., and Kamali, H. (2026). Bench4HLS: End-to-End Evaluation of LLMs in High-Level Synthesis Code Generation. *2026 Design, Automation & Test in Europe Conference (DATE)*, 1–7. https://doi.org/10.23919/date69613.2026.11539716
7. Wu, Y., Yu, X., Chen, H., Luo, Y., Tong, Y., and Ma, Y. (2025). PICBench: Benchmarking LLMs for Photonic Integrated Circuits Design. *2025 Design, Automation & Test in Europe Conference (DATE)*, 1–6. https://doi.org/10.23919/date64628.2025.10992854
8. Kim, J., Byun, J., Hwang, D., Park, S., and Song, H. O. (2026). Rule2DRC: Benchmarking LLM Agents for DRC Script Synthesis with Execution-Guided Test Generation. *Proceedings of the International Conference on Machine Learning (ICML)*. DOI not available; preprint: https://arxiv.org/abs/2605.15669
9. Liu, M., Pinckney, N., Khailany, B., and Ren, H. (2023). VerilogEval: Evaluating Large Language Models for Verilog Code Generation. *2023 IEEE/ACM International Conference on Computer Aided Design (ICCAD)*, 1–8. https://doi.org/10.1109/iccad57390.2023.10323812
10. Liu, S., Lu, Y., Fang, W., Li, M., and Xie, Z. (2024). OpenLLM-RTL: Open Dataset and Benchmark for LLM-Aided Design RTL Generation. *Proceedings of the 43rd IEEE/ACM International Conference on Computer-Aided Design*, 1–9. https://doi.org/10.1145/3676536.3697118
11. Nichols, D., Davis, J. H., Xie, Z., Rajaram, A., and Bhatele, A. (2024). Can Large Language Models Write Parallel Code?. *Proceedings of the 33rd International Symposium on High-Performance Parallel and Distributed Computing*, 281–294. https://doi.org/10.1145/3625549.3658689
12. Chen, L., Ahmed, N., Capotă, M., Willke, T., Hasabnis, N., and Jannesari, A. (2025). PCEBench: A Multi-Dimensional Benchmark for Evaluating Large Language Models in Parallel Code Generation. *2025 IEEE International Parallel and Distributed Processing Symposium (IPDPS)*, 546–557. https://doi.org/10.1109/ipdps64566.2025.00055
13. Yadav, D. and Mondal, S. (2025). Evaluating pre-trained Large Language Models on zero shot prompts for parallelization of source code. *Journal of Systems and Software*, 230, 112543. https://doi.org/10.1016/j.jss.2025.112543
14. Ouyang, A., Guo, S., Arora, S., Zhang, A. L., Hu, W., Ré, C., et al. (2025). KernelBench: Can LLMs Write Efficient GPU Kernels?. *Proceedings of the International Conference on Machine Learning (ICML)*. DOI not available; preprint: https://arxiv.org/abs/2502.10517
15. Nie, J., Wu, H., Lai, Y., Cao, Z., Zhang, C., Lou, B., et al. (2026). KernelCraft: Benchmarking for Agentic Close-to-Metal Kernel Generation on Emerging Hardware. *Proceedings of the International Conference on Machine Learning (ICML)*. DOI not available; preprint: https://arxiv.org/abs/2603.08721
16. Chong, Y. H., Wu, J., Zhang, Y., and Qu, P. (2026). Towards Feedback-to-Plan Decisions for Self-Evolving LLM Agents in CUDA Kernel Generation. *Proceedings of the International Conference on Machine Learning (ICML)*. DOI not available; preprint: https://arxiv.org/abs/2605.26720
17. Press, O., Amos, B., Zhao, H., Wu, Y., Ainsworth, S., Krupke, D., et al. (2026). AlgoTune: Can Language Models Speed Up General-Purpose Numerical Programs?. *Advances in Neural Information Processing Systems*, 38. DOI not available; preprint: https://arxiv.org/abs/2507.15887
18. Ma, J. J., Hashemi, M., Yazdanbakhsh, A., Swersky, K., Press, O., Li, E., et al. (2026). SWE-fficiency: Can Language Models Optimize Real-World Repositories on Real Workloads?. *Proceedings of the International Conference on Machine Learning (ICML)*. DOI not available; preprint: https://arxiv.org/abs/2511.06090
19. He, X., Liu, Q., Du, M., Yan, L., Fan, Z., Huang, Y., et al. (2026). SWE-Perf: Can Language Models Optimize Code Performance on Real-World Repositories?. *Proceedings of the International Conference on Machine Learning (ICML)*. DOI not available; preprint: https://arxiv.org/abs/2507.12415
20. Coignion, T., Quinton, C., and Rouvoy, R. (2025). When Faster Isn't Greener: The Hidden Costs of LLM-Based Code Optimization. *2025 40th IEEE/ACM International Conference on Automated Software Engineering (ASE)*, 1655–1666. https://doi.org/10.1109/ase63991.2025.00139
21. Erhabor, D., Udayashankar, S., Nagappan, M., and Al-Kiswany, S. (2025). Measuring the Runtime Performance of Code Produced with GitHub Copilot. *2025 IEEE/ACM 47th International Conference on Software Engineering (ICSE)*, 2062–2074. https://doi.org/10.1109/icse55347.2025.00059
22. Peters, G., Khatoonabadi, S., and Shihab, E. (2026). Evaluating the Use of LLMs for Automated DOM-Level Resolution of Web Performance Issues. *Proceedings of the 23rd International Conference on Mining Software Repositories*, 323–334. https://doi.org/10.1145/3793302.3793361
23. Kon, P. T. J., Liu, J., Qiu, Y., Fan, W., He, T., Lin, L., et al. (2024). IaC-Eval: A Code Generation Benchmark for Cloud Infrastructure-as-Code Programs. *Advances in Neural Information Processing Systems (NeurIPS)*. DOI not available.
24. Angi, A., Nedoshivina, L., Sacco, A., Braghin, S., and Purcell, M. (2025). A Perspective on LLM Data Generation with Few-shot Examples: from Intent to Kubernetes Manifest. *Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 6: Industry Track)*, 345–354. https://doi.org/10.18653/v1/2025.acl-industry.27
25. Wang, C., Scazzariello, M., Farshin, A., Ferlin, S., Kostić, D., and Chiesa, M. (2024). NetConfEval: Can LLMs Facilitate Network Configuration?. *Proceedings of the ACM on Networking*, 2(CoNEXT2), 1–25. https://doi.org/10.1145/3656296
26. Li, S., Jiang, J., Zhao, T., and Shen, J. (2026). OSVBench: Benchmarking LLMs on Specification Generation Tasks for Operating System Verification. *Proceedings of the AAAI Conference on Artificial Intelligence*, 40(37), 31698–31707. https://doi.org/10.1609/aaai.v40i37.40437
27. Wang, X., Wu, W., Narasayya, V., and Chaudhuri, S. (2026). Evaluating the Practical Effectiveness of LLM-Driven Index Tuning with Microsoft Database Tuning Advisor. *Proceedings of the VLDB Endowment*, 19(12), 4049–4062. https://doi.org/10.14778/3827998.3828015
28. Jha, S., Arora, R. R., Watanabe, Y., Yanagawa, T., Chen, Y., Clark, J., et al. (2025). ITBench: Evaluating AI Agents across Diverse Real-World IT Automation Tasks. *Proceedings of the International Conference on Machine Learning (ICML)*. DOI not available; preprint: https://arxiv.org/abs/2502.05352
29. Tang, Y., Zhu, K., Ruan, B., Zhang, C., Yang, M., Li, H., et al. (2026). DevOps-Gym: Benchmarking AI Agents in Software DevOps Cycle. *International Conference on Learning Representations (ICLR)*. DOI not available; preprint: https://arxiv.org/abs/2601.20882
30. Chen, Y., Shetty, M., Somashekar, G., Ma, M., Simmhan, Y., Mace, J., et al. (2025). AIOpsLab: A Holistic Framework to Evaluate AI Agents for Enabling Autonomous Clouds. *Proceedings of Machine Learning and Systems (MLSys)*. DOI not available; preprint: https://arxiv.org/abs/2501.06706
31. Qi, J., Luan, Z., Zhang, H., Huang, S., Fung, C., Tong, Y., et al. (2026). Can LLMs Really Recover Microservice Failures? A Recovery-Aware Evaluation of Diagnosis-to-Action Reasoning. *arXiv preprint arXiv:2607.04623*. https://arxiv.org/abs/2607.04623
32. Jadhav, P., Jin, H., Deelman, E., and Balaprakash, P. (2025). Evaluating the Efficacy of LLM-Based Reasoning for Multiobjective HPC Job Scheduling. *Proceedings of the SC '25 Workshops of the International Conference for High Performance Computing, Networking, Storage and Analysis*, 2234–2244. https://doi.org/10.1145/3731599.3767584
33. Klinaku, F., Summerer, T., and Becker, S. (2026). Let LLMs Autoscale Microservices: A Quantitative Evaluation of Architectures. *2026 IEEE 23rd International Conference on Software Architecture (ICSA)*, 237–244. https://doi.org/10.1109/icsa66085.2026.00030
