# Deployment Evidence Beyond Development Settings

Of the 317 archetype studies, 204 report benchmark or testbed evidence,
65 simulation, and 4 a sandbox. The remaining 44, listed here, report evidence
from a setting beyond these: 7 evaluate on production workloads or traces,
9 report externally reviewed use, 10 deploy or physically
realize a generated artifact, and 18 deploy a model-based component in production. Studies
are grouped by that coding, which records the strongest setting each study reports.

Each row summarizes what ran, who performs the consequential action, the reported scale or duration, and the
outcomes assessed. Missing deployment measures are identified where relevant. Scale, duration, and acceptance
measures help distinguish the evidence provided by different deployment settings. The column `C` gives the archetype. The underlying coding is in
[`../data/coding/archetype-studies.csv`](../data/coding/archetype-studies.csv), field `evidence_level`.

| Study | C | What ran and who acts | Scale / duration | What the evidence measures |
|---|---|---|---|---|
| **Model-based component deployed in production (18)** | | | | |
| RCACopilot [1] | C5 | Root-cause category prediction; OCEs review and mitigate | Predictor: several months, one service | Micro-/macro-F1 on offline replay; OCE feedback qualitative |
| RCAgent [2] | C5 | Read-only diagnosis agent; SRE team acts | First two weeks of deployment | SRE-rated helpfulness 2.92/5 vs. 1.36 for ReAct |
| FlowXpert [3] | C5 | Troubleshooting workflows; OCEs accept and execute | 10 weeks; 34,488 tickets | About 80% weekly OCE acceptance |
| Confucius [4] | C4 | Intent-to-DSL agents; existing tools execute, with human approval for highly sensitive tasks | Two years; 4.16K users, 64 use cases | Adoption; survey-reported hours saved |
| OncallX [5] | C5 | On-call answers and automatic ticket triage; humans mitigate | Two months | Response and triage latency only |
| BiAn [6] | C5 | Failure-localization ranking; operators act | 10 months; one global network | A/B time to root cause −20.5% vs. manual |
| Triangle [7] | C5 | Automatic incident routing; humans mitigate | Two organizations; six services | Routing accuracy 64–97%; before/after TTE, uncontrolled |
| AIDA [8] | C5 | Post-incident RCA reports with abstention; operators act | Over one year; 846 cases | Precision 95.4%; median time to RCA 72.6 h (manual) to 1.6 min |
| XiHe [9] | C5 | Root-causing graphs in operator dashboard; actuation prohibited | 12 months; 3,000+ incidents | A/B root-causing time −25.8% |
| IntelliTopo [10] | C3 | IaC service deploying simulation topologies on the authors' PaaS | Three months; 50+ tasks | 50-user alignment survey (85% little or no change); timing only on an offline 60-case set |
| DBAgent [11] | C5 | Diagnosis and remedies; human approval for state changes | Two sites, Feb–Sep 2025 | 60% fewer human-handled consultation tickets (ERP); 87% lower handling time (bank); before/after |
| LogPilot [12] | C5 | Alert-diagnosis reports to OCEs | 12 services; 3,500+ alerts, June–July 2025 | 84.21% of reports accepted |
| Huang et al. [13] | C5 | Advisory diagnosis reports triggered by alerts | Four systems, since June 2025 | >80% accuracy; diagnosis >1 h to <5 min; aggregate, not controlled |
| KAT [14] | C5 | Troubleshooting root cause and repair steps in the operator interface; O&M staff act | 10 months; provincial telecom support system, 35M users, ~80k errors/month; later 15 more provinces | Mean error-resolution time 51.4 h to 5.9 h, before/after, uncontrolled; satisfaction ratings |
| OpsAgent [15] | C5 | Real-time diagnosis reports; frontline OCEs carry out every mitigation | 53 days; 10,492 production incidents, about 2.5 × 10⁴ instances | 84.09% accuracy (OCE-confirmed by mitigation); manual resolution ~2.5 h (3 OCEs) vs. 126 s per diagnosis, not like-for-like |
| MonitorAssistant [16] | C5 | Monitor configuration and detector patches installed in the monitoring layer; engineer confirms patches | Scale and duration not reported | Qualitative case studies only |
| GaussMaster [17] | C5 | Database copilot invoking diagnostic tools; claims zero human intervention in 34+ scenarios, repair authority not evidenced | Banking (e.g., Agricultural Bank of China); 1,614 bank questions; duration not reported | Self-reported accuracy; no evaluation protocol given |
| Artanis [18] | C3 | Intent-derived configuration updates pushed to a network controller; a learned GNN verifier is the gate; "minimal manual involvement" (text), none (Table V) | Enterprise network, hundreds of nodes; duration and intent volume not reported | 1.61 update loops, 12.84 s per update; no service-level outcome |
| **Generated artifact deployed or physically realized (10)** | | | | |
| AlphaEvolve [19] | C3 | Evolved Borg scheduling and kernel-tiling heuristics; human rollout decision; the heuristics run with no further model inference | Fleet-wide; Gemini training pipeline | Post-rollout measurement: 0.7% of fleet compute recovered, author-reported |
| ECO [20] | C3 | Efficiency commits after CI and code-owner review; release pipeline deploys | Over one year; 6.4k+ commits | Profiler-measured savings; revert rate 0.12–0.16% |
| KernelEvolve [21] | C3 | Selected kernels in production serving with fallback dispatch; rollout process not described | Continuous, by the authors' account | Speedups on production shapes; no fleet-level impact |
| AliYANG [22] | C4 | Validated, engineer-reviewed YANG models and translators; deterministic system applies configurations | Host system: three years, hundreds of thousands of devices | Self-reported 4–6× less onboarding effort |
| ChatCPU [23] | C3 | Generated CPU taped out | One MPW chip | No post-silicon results |
| AMS-IO-Agent [24] | C4 | Generated I/O ring in a tape-out after human review | One 28 nm chip | Silicon measured functional |
| AutoRF [25] | C3 | RF designs fabricated by the authors | Nine prototypes | Physical measurements |
| IoTGen [26] | C3 | PCBs fabricated by the authors | Two boards | Functional test |
| CLST workflow [27] | C3 | Generated RISC-V core on an FPGA after manual fixes | One board | On-board test |
| Crucible [28] | C3 | LLM-tuned ABR algorithms run in a real-world Dash.js test; researchers run it | Public WiFi; scale and variance not reported | QoE of tuned HYB and BBA 1.72 vs. 1.40 and 1.56 untuned |
| **Human-reviewed external use (9)** | | | | |
| COMET [29] | C1 | Triage keywords and team recommendation on incident pages | Two services; 6+ months | Online ACC@1 0.61 vs. 0.47 rule-based |
| ScriptSmith [30] | C3 | Script recommendations; SRE review | Six months internal use | No production outcome reported |
| StepFly [31] | C5 | Guide-driven read-only diagnosis; SREs review | 170+ monitors, 70+ teams | Median mitigation time −34%, method not described |
| LPO [32] | C4 | Alive2-checked missed-optimization reports; maintainers patch | LLVM upstream | 62 reported, 28 confirmed, 13 fixed |
| MeshAgent [33] | C4 | Web deployment for a user study at a network provider | 20 participants (15 interns); 200 queries | User preference and accuracy |
| SemOpt [34] | C3 | Optimization pull requests | Five projects | Accepted in two; others under review |
| CausalDX [35] | C5 | Diagnoses on live incidents; human-gated mitigation | 118 responses | 74% rated useful vs. 61% for prior rule-based output |
| ActionNex [36] | C5 | Next-action recommendations for outage responders; humans execute | Production pilot; no duration, case count or usage statistic reported | Offline replay only: precision 71.4%, recall 52.8–54.8% |
| Roy et al. [37] | C5 | ReAct agent with the team's diagnostic tools, demonstrated to OCEs in a chat interface | 4-week collaboration; demos on a small set of incidents, one team | Qualitative case study; the authors call it a first step |
| **Evaluation on production workloads or traces (7)** | | | | |
| E2ETune [38] | C3 | Knob configurations; internal development environment | Two company workloads | Workload performance |
| R-Bot [39] | C3 | Query rewrites on a bank dataset (deployment claimed) | 20 slow queries | Total latency 9.23 h to 4.37 h |
| AgentTune [40] | C3 | Tuning sessions in a separate production environment | Two workloads | Workload performance |
| LeJOT-AutoML [41] | C1 | Features for a job-time predictor; live or replay unclear | One deployment setting | Cost saving 19.01% vs. 27.94% manual |
| LLMIA [42] | C3 | Index advice in a private environment | Two company workloads | Workload performance |
| MVGPT [43] | C2 | Materialized views on historical logs of Alibaba's advertising platform; daily automatic creation claimed, not measured | Last month of the workload as test set | Offline hit rate and saved query time only |
| PROMPTS [44] | C3 | Sharding-configuration proposals for production TPU jobs; engineers apply through the existing workflow | Eight engineer-submitted cases | Top proposal matched the adopted configuration in 7 of 8; 69% of proposals compiled |

## References

1. Chen, Y., Xie, H., Ma, M., Kang, Y., Gao, X., Shi, L., et al. (2024). Automatic Root Cause Analysis via Large Language Models for Cloud Incidents. *Proceedings of the Nineteenth European Conference on Computer Systems*, 674–688. https://doi.org/10.1145/3627703.3629553
2. Wang, Z., Liu, Z., Zhang, Y., Zhong, A., Wang, J., Yin, F., et al. (2024). RCAgent: Cloud Root Cause Analysis by Autonomous Agents with Tool-Augmented Large Language Models. *Proceedings of the 33rd ACM International Conference on Information and Knowledge Management*, 4966–4974. https://doi.org/10.1145/3627673.3680016
3. Shi, B., Luo, Y., Wang, J., Zhao, Y., Zhang, S., Hao, B., et al. (2025). FlowXpert: Expertizing Troubleshooting Workflow Orchestration with Knowledge Base and Multi-Agent Coevolution. *Proceedings of the 31st ACM SIGKDD Conference on Knowledge Discovery and Data Mining V.2*, 4839–4850. https://doi.org/10.1145/3711896.3737221
4. Wang, Z., Lin, S., Yan, G., Ghorbani, S., Yu, M., Zhou, J., et al. (2025). Intent-Driven Network Management with Multi-Agent LLMs: The Confucius Framework. *Proceedings of the ACM SIGCOMM 2025 Conference*, 347–362. https://doi.org/10.1145/3718958.3750537
5. Fu, R., Zhang, Y., Che, Z., Wu, X., Zhong, Z., Ren, Z., et al. (2025). LLM-Powered Multi-Agent Collaboration for Intelligent Industrial On-Call Automation. *2025 40th IEEE/ACM International Conference on Automated Software Engineering (ASE)*, 2222–2234. https://doi.org/10.1109/ase63991.2025.00184
6. Wang, C., Zhang, X., Lu, R., Lin, X., Zeng, X., Zhang, X., et al. (2025). Towards LLM-Based Failure Localization in Production-Scale Networks. *Proceedings of the ACM SIGCOMM 2025 Conference*, 496–511. https://doi.org/10.1145/3718958.3750505
7. Yu, Z., Fang, A., Ma, M., Walia, J. S., Zhang, C., Chi, S., et al. (2025). Triangle: Empowering Incident Triage with Multi-Agent. *2025 40th IEEE/ACM International Conference on Automated Software Engineering (ASE)*, 674–686. https://doi.org/10.1109/ase63991.2025.00062
8. Xu, H., Zeng, X., Zhang, X., Zhang, X., Lv, Y., Zhang, P., et al. (2026). AIDA: Accelerating Root Cause Analysis for Multi-Vendor Device Failures with LLM-Powered Reasoning. *Proceedings of the ACM SIGCOMM 2026 Conference*, 770–786. https://doi.org/10.1145/3789240.3829126
9. Ren, Y., Lin, X., Wang, C., Chen, L., Wang, S., Gao, K., et al. (2026). Networked Agent Memory and Causality Representation: Experiences towards Interpretable Cloud-Scale Root-Causing. *Proceedings of the ACM SIGCOMM 2026 Conference*, 787–808. https://doi.org/10.1145/3789240.3829145
10. Shao, M., Liu, Z., Han, W., Gao, C., Liu, J., and Liao, Q. (2025). IntelliTopo: An IaC Generation Service for Industrial Network Topology Construction. *2025 40th IEEE/ACM International Conference on Automated Software Engineering (ASE)*, 3605–3615. https://doi.org/10.1109/ase63991.2025.00298
11. Chen, X., Chen, J., Liu, S., Xia, Y., Liang, Z., Qin, X., et al. (2026). DBAgent: An RL-Based Agent for Autonomous Database Operations and Maintenance. *Proceedings of the VLDB Endowment*, 19(12), 3928–3940. https://doi.org/10.14778/3827998.3828006
12. Jiang, Z., Liu, J., Li, Y., Huang, H., He, X., Zhang, T., et al. (2025). LogPilot: Intent-aware and Scalable Alert Diagnosis for Large-scale Online Service Systems. *2025 40th IEEE/ACM International Conference on Automated Software Engineering (ASE)*, 3299–3310. https://doi.org/10.1109/ase63991.2025.00272
13. Huang, H., Lyu, J., Lai, S., Jiang, Z., Chen, P., and Lyu, M. R. (2026). Reliable Orchestration of Specialized Multi-Agents for Cloud Incident Diagnosis. *2026 IEEE International Conference on Web Services (ICWS)*, 1538–1548. https://doi.org/10.1109/icws72778.2026.00187
14. Qian, K., Lyu, F., Wu, H., Gao, J., Li, S., Wu, F., et al. (2026). KAT: Knowledge-Context Augmentation for Evolving LLM-Based Telecom Troubleshooting. *IEEE INFOCOM 2026 - IEEE Conference on Computer Communications*, 1–10. https://doi.org/10.1109/infocom59046.2026.11571301
15. Luo, Y., Jiang, J., Feng, J., Tao, L., Zhang, Q., Wen, X., et al. (2026). OpsAgent: An Evolving Multi-agent System for Incident Management in Microservices. *Proceedings of the 41st IEEE/ACM International Conference on Automated Software Engineering*, 3896–3907. DOI not available; preprint: https://arxiv.org/abs/2510.24145
16. Yu, Z., Ma, M., Zhang, C., Qin, S., Kang, Y., Bansal, C., et al. (2024). MonitorAssistant: Simplifying Cloud Service Monitoring via Large Language Models. *Companion Proceedings of the 32nd ACM International Conference on the Foundations of Software Engineering*, 38–49. https://doi.org/10.1145/3663529.3663826
17. Zhou, W., Sun, J., Zhou, X., Li, G., Liu, L., Wu, H., et al. (2025). GaussMaster: An LLM-based Database Copilot System. *arXiv preprint arXiv:2506.23322*. https://arxiv.org/abs/2506.23322
18. Guo, L., Yan, Y., Qi, Q., Sun, H., Peng, Y., Zhuang, Z., et al. (2026). From Generation to Guarantee: Intent-Based Configuration Update with Verification Feedback. *IEEE INFOCOM 2026 - IEEE Conference on Computer Communications*, 1–10. https://doi.org/10.1109/infocom59046.2026.11571454
19. Novikov, A., Vu, N., Eisenberger, M., Dupont, E., Huang, P., Wagner, A., et al. (2025). AlphaEvolve: A coding agent for scientific and algorithmic discovery. *arXiv preprint arXiv:2506.13131*. https://arxiv.org/abs/2506.13131
20. Lin, H., Maas, M., Roquemore, M., Hasanzadeh, A., Lewis, F., Simonson, Y., et al. (2026). ECO: An LLM-Driven Efficient Code Optimizer for Warehouse Scale Computers. *USENIX Symposium on Operating Systems Design and Implementation (OSDI)*. DOI not available; preprint: https://arxiv.org/abs/2503.15669
21. Liao, G., Qin, H., Wang, Y., Golden, A., Kuchnik, M., Yetim, Y., et al. (2026). KernelEvolve: Scaling Agentic Kernel Coding for Heterogeneous AI Accelerators at Meta. *2026 ACM/IEEE 53rd Annual International Symposium on Computer Architecture (ISCA)*, 733–747. https://doi.org/10.1109/isca66397.2026.00063
22. Yu, M., Zhang, X., An, Z., Wang, E., and Zheng, B. (2026). Evolution of AliYANG: Model-driven and LLM-assisted Network Configuration Management. *Proceedings of the ACM SIGCOMM 2026 Conference*, 1724–1738. https://doi.org/10.1145/3789240.3829193
23. Wang, X., Wan, G., Wong, S., Zhang, L., Liu, T., Tian, Q., et al. (2024). ChatCPU: An Agile CPU Design and Verification Platform with LLM. *Proceedings of the 61st ACM/IEEE Design Automation Conference*, 1–6. https://doi.org/10.1145/3649329.3658493
24. Zhang, Z., Li, X., Liu, S., Zhang, A., Jie, L., and Sun, N. (2026). AMS-IO-Bench and AMS-IO-Agent: Benchmarking and Structured Reasoning for Analog and Mixed-Signal Integrated Circuit Input/Output Design. *Proceedings of the AAAI Conference on Artificial Intelligence*, 40(2), 1579–1586. https://doi.org/10.1609/aaai.v40i2.37134
25. Ma, R., Qiu, L., Hu, W., Wang, J., Song, Y., and Pan, H. (2026). AutoRF: Towards an Agentic Framework for Automated RF Hardware Design. *Proceedings of the 24th Annual International Conference on Mobile Systems, Applications and Services*, 279–293. https://doi.org/10.1145/3745756.3809204
26. Luo, Q., Ma, R., Zhang, X., and Qiu, L. (2026). [Emerging Ideas] IoTGen: Towards LLM-diriven IoT Hardware Generation. *Proceedings of the 24th Annual International Conference on Mobile Systems, Applications and Services*, 792–807. https://doi.org/10.1145/3745756.3809239
27. El-Helwani, T. and Khalid, M. A. S. (2026). LLM-Aided Design and Evaluation of a RISC-V Processor. *IEEE Access*, 14, 93247–93283. https://doi.org/10.1109/access.2026.3705296
28. Jia, L., Li, C., Houde, Q., Huang, T., Liu, J., and Sun, L. (2026). Crucible: Quantifying the Potential of Control Algorithms through LLM Agents. *Advances in Neural Information Processing Systems*, 38, 123043–123067. DOI not available; preprint: https://arxiv.org/abs/2510.18491
29. Wang, Z., Li, J., Ma, M., Li, Z., Kang, Y., Zhang, C., et al. (2024). Large Language Models Can Provide Accurate and Interpretable Incident Triage. *2024 IEEE 35th International Symposium on Software Reliability Engineering (ISSRE)*, 523–534. https://doi.org/10.1109/issre62328.2024.00056
30. Aggarwal, P., Chatterjee, O., Dai, T., Samanta, S., Mohapatra, P., Kar, D., et al. (2025). ScriptSmith: A Unified LLM Framework for Enhancing IT Operations via Automated Bash Script Generation, Assessment, and Refinement. *Proceedings of the AAAI Conference on Artificial Intelligence*, 39(28), 28829–28835. https://doi.org/10.1609/aaai.v39i28.35147
31. Mao, J., Li, L., Gao, Y., Peng, Z., He, S., Zhang, C., et al. (2026). Agentic Troubleshooting Guide Automation for Incident Management. *Proceedings of the ACM on Software Engineering*, 3(FSE), 3070–3092. https://doi.org/10.1145/3808143
32. Xu, Z., Xu, H., Tian, Y., Zhou, X., and Sun, C. (2026). Leveraging Large Language Models to Detect Missed Peephole Optimizations. *Proceedings of the 31st ACM International Conference on Architectural Support for Programming Languages and Operating Systems, Volume 2*, 1136–1150. https://doi.org/10.1145/3779212.3790184
33. Zhou, Y., Hsieh, K., Mani, S. K., Kandula, S., and Liu, Z. (2026). MeshAgent: Enabling Reliable Network Management with Large Language Models. *Proceedings of the ACM on Measurement and Analysis of Computing Systems*, 9(3), 1–36. https://doi.org/10.1145/3801489.3806880
34. Zhao, Y., Xiao, Y., Xiao, Q., Zhang, Z., and Xiong, Y. (2026). SemOpt: LLM-Driven Code Optimization via Rule-Based Analysis. *ACM Transactions on Software Engineering and Methodology*. https://doi.org/10.1145/3820167
35. Chang, Z., Wu, Y., Feng, H., Li, Y., Fang, Y., Liu, L., et al. (2026). CausalDX: Diagnosing Long-Tail and Cascading Cloud Incidents With LLM-Guided Causal Reasoning. *IEEE Transactions on Knowledge and Data Engineering*, 38(10), 6424–6438. https://doi.org/10.1109/tkde.2026.3722256
36. Lin, Z., Hu, H., Hao, M., Zhang, X., Zhang, R., Li, J., et al. (2026). ActionNex: A Virtual Outage Manager for Cloud Computing. *arXiv preprint arXiv:2604.03512*. https://arxiv.org/abs/2604.03512
37. Roy, D., Zhang, X., Bhave, R., Bansal, C., Las-Casas, P., Fonseca, R., et al. (2024). Exploring LLM-Based Agents for Root Cause Analysis. *Companion Proceedings of the 32nd ACM International Conference on the Foundations of Software Engineering*, 208–219. https://doi.org/10.1145/3663529.3663841
38. Huang, X., Li, H., Zhang, J., Zhao, X., Yao, Z., Li, Y., et al. (2025). E2ETune: End-to-End Knob Tuning via Fine-tuned Generative Language Model. *Proceedings of the VLDB Endowment*. https://doi.org/10.14778/3773731.3773732
39. Sun, Z., Zhou, X., Li, G., Yu, X., Feng, J., and Zhang, Y. (2025). R-Bot: An LLM-based Query Rewrite System. *Proceedings of the VLDB Endowment*, 18(12), 5031–5044. https://doi.org/10.14778/3750601.3750625
40. Li, Y., Li, H., Zhang, J., Borovica-Gajic, R., Wang, S., Zhang, T., et al. (2025). AgentTune: An Agent-Based Large Language Model Framework for Database Knob Tuning. *Proceedings of the ACM on Management of Data*, 3(6), 1–29. https://doi.org/10.1145/3769758
41. Ma, L., Hu, Y., Ren, Y., Wu, F., and Li, X. (2026). LeJOT-AutoML: LLM-Driven Feature Engineering for Job Execution Time Prediction in Databricks Cost Optimization. *IEEE INFOCOM 2026 - IEEE Conference on Computer Communications*, 1–6. https://doi.org/10.1109/infocom59046.2026.11571455
42. Zhao, X., Huang, X., Li, H., Zhang, J., Wang, S., Zhang, T., et al. (2026). Llmia: an Out-Of-The-Box Index Advisor Via in-Context Learning With Llms. *2026 IEEE 42nd International Conference on Data Engineering (ICDE)*, 2957–2970. https://doi.org/10.1109/icde65706.2026.00220
43. Han, Y., Li, G., Xu, W., Ran, X., Gong, Z., Guo, W., et al. (2026). MVGPT: Generative Materialized View Forecasting. *2026 IEEE 42nd International Conference on Data Engineering (ICDE)*, 155–168. https://doi.org/10.1109/icde65706.2026.00019
44. Ding, Y., Han, R., Zhang, X., and Chen, X. (2026). PROMPTS: Performance Optimization via Multi-Agent Planning for LLM Training and Serving. *Proceedings of Machine Learning and Systems (MLSys)*. DOI not available.
