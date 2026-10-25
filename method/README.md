# Search Specification

This folder documents the identification and selection procedure of the survey. This file specifies the
bibliographic source, the date restriction, the title-matching rules, the retrieval routes, and the complete search
vocabularies, so that the title query can be re-executed against the same source. The remaining files in this folder
document the subsequent stages:

- [`eligibility-criteria.md`](eligibility-criteria.md) states the five inclusion criteria (P1–P5) applied after
  title and abstract screening, together with the scope clarifications adopted during full-text review.
- [`coding-scheme.md`](coding-scheme.md) defines the classification and coding applied to each included work and
  every field of the released data files in [`../data/`](../data/).

## Bibliographic Source

The search was executed against the DBLP persistent monthly snapshot of 1 September 2026
(`dblp-2026-09-01.xml.gz`, https://doi.org/10.4230/dblp.xml.2026-09-01; MD5
`41abb87b4e8b8a2e3c470efd6528ad88`). The parser retains articles, conference papers (`inproceedings`), and book chapters
(`incollection`). Records marked withdrawn, software, data, or encyclopedia are excluded before title matching.
After restriction by publication type and date, 2,414,509 records remained.

## Date Restriction

Records with publication years 2023 through 2027 were retained; the upper bound admits forthcoming-issue records that
DBLP already dates to 2027. Records from 2022 were retained only when dated December 2022, as established by the
DBLP month field, an arXiv identifier beginning with `2212`, or the publication date registered for the DOI. Records
from 2022 whose month could not be determined were retained and flagged for manual verification during screening.

The snapshot date bounds primary-search indexing, rather than every record's bibliographic issue year.
Snowballed works were retained when their venue version had been published by 15 September 2026.

## Title Matching

Each title was converted to lower case and segmented into alphanumeric words. Unless marked otherwise, a term
matches when it occurs at the beginning of a word, so that a term such as `autoscal` matches both "autoscaling" and
"autoscaler". A multi-word term matches only when its words occur consecutively. Two markers modify this default: a
trailing `$` requires a whole-word match (`rag$` matches "RAG" but not "ragged"), and a leading `*` permits the term
to begin inside a word (`*agent` matches "RCAgent").

## Retrieval Routes

A title was retained if it satisfied at least one of the seven routes below, each of which is a conjunction
of vocabularies; a route is satisfied when the title contains at least one term from each vocabulary it names. All
matching routes and matched terms were recorded for each retained title. The query returned 81,132 records,
corresponding to 69,456 unique titles.

| Route | Condition |
|---|---|
| R1 | Strong language-model terms and specific systems terms |
| R2 | Strong language-model terms and general systems terms |
| R3 | Weak language-model terms and specific systems terms |
| R4 | Model-name terms and specific systems terms |
| R5 | Method terms and specific systems terms |
| R6 | AI-assisted terms and hardware terms |
| R7 | Standalone phrases |

## Search Vocabularies

The nine vocabularies comprise 705 terms in total. Terms are listed exactly as applied, including the matching
markers defined above; a term may appear in more than one vocabulary.

| Vocabulary (terms) | Terms |
|---|---|
| Strong language-model terms (20) | `llm`; `language model`; `gpt`; `chatgpt`; `generative ai`; `genai`; `foundation model`; `copilot`; `codex`; `claude`; `gemini`; `llama`; `mllm`; `*llm`; `*gpt`; `vlm`; `vision language model`; `vision language`; `multimodal language model`; `*copilot` |
| Weak language-model terms (6) | `agent`; `*agent`; `large model`; `reasoning model`; `code model`; `slm$` |
| Model-name terms (13) | `bert`; `*bert`; `roberta`; `t5$`; `bart$`; `codebert`; `codet5`; `starcoder`; `deepseek`; `qwen`; `mistral`; `gemma`; `phi$` |
| Method terms (26) | `natural language`; `retrieval augmented`; `rag$`; `chain of thought`; `fine tun`; `finetun`; `in context`; `prompt`; `instruction tun`; `self reflection`; `reflection`; `reinforcement learning from`; `generative ai`; `ai agent`; `language based`; `neuro symbolic`; `neural symbolic`; `code generation`; `tool augmented`; `tool using`; `self refine`; `self refinement`; `self correct`; `self correction`; `few shot`; `zero shot` |
| AI-assisted terms (3) | `ai assisted`; `ai aided`; `ai powered` |
| Specific systems terms (413) | `3d ic`; `5g$`; `6g$`; `accelerator`; `adaptation rule`; `adder`; `aiops`; `alert`; `algorithm discovery`; `analog`; `anomal`; `ansible`; `asic$`; `assertion`; `auto tun`; `autonomous network`; `autoscal`; `autotun`; `bgp$`; `binary translation`; `cach`; `cache eviction`; `cache manag`; `cache polic`; `caching polic`; `cardinality`; `cgra`; `chaos engineering`; `chip`; `chisel`; `ci cd`; `circuit`; `cloud`; `cloud architecture`; `cloud comput`; `cloud incident`; `cloud infrastructure`; `cloud native`; `cloud operation`; `cloud reliab`; `cloud resource`; `cloud system`; `cluster`; `cluster manag`; `cluster schedul`; `code efficien`; `code optimi`; `collective communication`; `communication network`; `compilation`; `compiler`; `compiler tuning`; `computer architecture`; `computer network`; `computer system`; `computing system`; `config$`; `configur`; `configuration tuning`; `congestion`; `container`; `coverage closure`; `cuda`; `data center`; `data corruption`; `data lake`; `data management`; `data management system`; `data pipeline`; `data system`; `database`; `database tuning`; `datacenter`; `dbms`; `decompil`; `deploy`; `design automation`; `design exploration`; `design flow`; `design rule`; `design space exploration`; `design validation`; `design verification`; `device driver`; `devops`; `diagnos`; `distinct values`; `distributed system`; `dns$`; `docker`; `drc$`; `driver`; `dse$`; `dvfs`; `ebpf`; `eda$`; `edge comput`; `efficient code`; `electronic design`; `embedded`; `energy concern`; `energy efficien`; `etl$`; `execution time`; `faas$`; `failure`; `failure analy`; `failure diagnos`; `failure localiz`; `failure predict`; `failure recovery`; `fault`; `fault diagnos`; `fault injection`; `fault locali`; `fault toleran`; `file system`; `filesystem`; `finite state machine`; `firewall`; `firmware`; `flash`; `flash memory`; `floorplan`; `formal verification`; `fortran`; `fpga`; `front end design`; `fsm$`; `gitops`; `gpu`; `gpu cluster`; `gpu code`; `gpu kernel`; `gpu optimi`; `gpu program`; `green`; `hardware`; `hardware verification`; `hdl$`; `heuristic`; `heuristic design`; `heuristic discovery`; `high level synthesis`; `high performance comput`; `high performance network`; `hls$`; `hotspot`; `hpc$`; `hypervisor`; `iac$`; `ibn$`; `incident`; `index recommend`; `index selection`; `index tuning`; `index$`; `indexes$`; `inefficien`; `inference cluster`; `infrastructure`; `infrastructure as code`; `intent`; `intent acquisition`; `intent assurance`; `intent based`; `intent drift`; `intent driven`; `intent management`; `intent translation`; `internet measurement`; `iot$`; `it automation`; `it operation`; `itops`; `job schedul`; `join order`; `k8s`; `kernel`; `key value`; `knob`; `knob tuning`; `kubernetes`; `layout`; `library characterization`; `linux`; `lithograph`; `llvm`; `load balanc`; `lock contention`; `log analy`; `log pars`; `log$`; `logging`; `logic synthesis`; `logs$`; `loop`; `loop nest`; `loop optimi`; `loop transform`; `lsm$`; `mape k`; `materialized view`; `microarchitecture`; `microservice`; `misconfigur`; `mlir`; `monitor`; `mpi$`; `netlist`; `network`; `network automation`; `network configuration`; `network design`; `network digital twin`; `network emulation`; `network experiment`; `network function`; `network intent`; `network management`; `network measurement`; `network operation`; `network optimi`; `network planning`; `network protocol`; `network slic`; `network traffic`; `network troubleshoot`; `network verification`; `networking`; `nfv$`; `o ran`; `observab`; `offload`; `on call`; `opc$`; `opencl`; `openmp`; `operating system`; `optical network`; `os$`; `outage`; `packet`; `parallel`; `parallel code`; `parallel comput`; `parallel program`; `paralleli`; `parameter tuning`; `partition`; `peephole`; `performance analy`; `performance bug`; `performance issue`; `performance model`; `performance optimi`; `performance regression`; `performance tuning`; `physical design`; `placement`; `plc$`; `power estimation`; `power management`; `ppa$`; `pqc$`; `pragma`; `prefetch`; `processor`; `program optimi`; `protocol`; `queries`; `query`; `query engine`; `query execution`; `query optimi`; `query plan`; `query processing`; `query rewrit`; `ran$`; `rapp`; `rca$`; `real time`; `real time system`; `reference model`; `register allocation`; `reliability engineering`; `remediat`; `resource allocation`; `resource management`; `risc v`; `root cause`; `router`; `routing`; `rtl$`; `rtls$`; `rtos`; `runbook`; `runtime memory`; `runtime performance`; `sat solv`; `schedul`; `scheduler`; `scheduling algorithm`; `scheduling polic`; `sdn$`; `self adaptive`; `semiconductor`; `serverless`; `silicon`; `site reliability`; `slicing`; `soc$`; `software defined`; `space planning`; `sql$`; `sre$`; `ssd$`; `standard cell`; `storage`; `superoptimi`; `sva$`; `svrf`; `sycl`; `synthesizable`; `system behavio`; `system design`; `system level`; `system tuning`; `systemc`; `systems heuristic`; `systems optimi`; `systems research`; `systemverilog`; `technology mapping`; `telecom`; `telemetry`; `tensor program`; `terraform`; `test program`; `test stimul`; `testbench`; `testsuite`; `thermal`; `timing`; `timing analy`; `timing closure`; `timing predict`; `traces$`; `tracing`; `traffic`; `traffic engineering`; `triton$`; `troubleshoot`; `tuning`; `vectoriz`; `verilog`; `vhdl`; `virtual machine`; `vnf$`; `web performance`; `wireless`; `wireless network`; `workload`; `xapp`; `vlsi`; `ic$`; `integrated circuit`; `cad$`; `tcad`; `schematic`; `mixed signal`; `analog layout`; `circuit sizing`; `device sizing`; `gate sizing`; `cell sizing`; `signoff`; `static timing`; `sta$`; `clock tree`; `place and route`; `pnr$`; `route$`; `dft$`; `design for test`; `atpg`; `scan chain`; `hardware test`; `test generation`; `lvs$`; `layout versus schematic`; `spice$`; `pdk$`; `process design kit`; `cdc$`; `clock domain crossing`; `rdc$`; `reset domain crossing`; `uvm$`; `post silicon`; `silicon debug`; `bringup`; `bring up`; `tapeout`; `tape out`; `noc$`; `network on chip`; `on chip network`; `interconnect`; `hardware security`; `hardware debug`; `device optimi`; `device design` |
| General systems terms (67) | `algorithm`; `architecture`; `asic`; `assistant`; `automat`; `autonomous`; `backend design`; `benchmark`; `characterization`; `code`; `compression`; `concolic`; `config`; `consensus`; `copilot`; `coverage`; `data plane`; `dataplane`; `deployment`; `design`; `efficien`; `energy`; `handover`; `heterogeneous`; `integration test`; `intelligent`; `io ring`; `ir$`; `latency`; `library generation`; `lock`; `lowering`; `management`; `measurement`; `memory`; `microelectronic`; `mitigation`; `ml library`; `model based testing`; `monitoring`; `multimodal chip`; `operation`; `operator`; `optimi`; `performance`; `plan`; `platform`; `profiling`; `program`; `repair operation`; `runtime`; `schema`; `shift left`; `simulat`; `software`; `sraf`; `synthesis`; `system`; `systems$`; `task assign`; `testability`; `throughput`; `trac`; `transcompil`; `validation`; `verification`; `wlan` |
| Hardware terms (122) | `3d ic`; `accelerator`; `adder`; `analog`; `asic$`; `assertion`; `cgra`; `chip`; `chisel`; `circuit`; `computer architecture`; `coverage closure`; `design automation`; `design exploration`; `design flow`; `design rule`; `design space exploration`; `design validation`; `design verification`; `drc$`; `dse$`; `eda$`; `electronic design`; `embedded`; `finite state machine`; `firmware`; `floorplan`; `formal verification`; `fpga`; `front end design`; `fsm$`; `hardware`; `hardware verification`; `hdl$`; `high level synthesis`; `hls$`; `hotspot`; `layout`; `library characterization`; `lithograph`; `logic synthesis`; `microarchitecture`; `netlist`; `opc$`; `physical design`; `placement`; `power estimation`; `ppa$`; `pragma`; `processor`; `reference model`; `risc v`; `rtl$`; `rtls$`; `semiconductor`; `silicon`; `soc$`; `standard cell`; `sva$`; `svrf`; `synthesizable`; `systemc`; `systemverilog`; `technology mapping`; `test program`; `test stimul`; `testbench`; `timing`; `timing analy`; `timing closure`; `timing predict`; `verilog`; `vhdl`; `vlsi`; `ic$`; `integrated circuit`; `cad$`; `tcad`; `schematic`; `mixed signal`; `analog layout`; `circuit sizing`; `device sizing`; `gate sizing`; `cell sizing`; `signoff`; `static timing`; `sta$`; `clock tree`; `place and route`; `pnr$`; `route$`; `dft$`; `design for test`; `atpg`; `scan chain`; `hardware test`; `test generation`; `lvs$`; `layout versus schematic`; `spice$`; `pdk$`; `process design kit`; `cdc$`; `clock domain crossing`; `rdc$`; `reset domain crossing`; `uvm$`; `post silicon`; `silicon debug`; `bringup`; `bring up`; `tapeout`; `tape out`; `noc$`; `network on chip`; `on chip network`; `interconnect`; `hardware security`; `hardware debug`; `device optimi`; `device design` |
| Standalone phrases (35) | `verilog`; `systemverilog`; `rtl code`; `rtl generation`; `rtl design`; `hdl code`; `hardware code`; `hardware design generation`; `cuda kernel`; `gpu kernel`; `kernel generation`; `ebpf program`; `network configuration synthesis`; `configuration synthesis`; `hls pragma`; `assertion generation`; `query optimizer`; `natural language interface`; `rtl$`; `hdl$`; `eda$`; `cuda`; `ebpf`; `kernel optimi`; `intent based`; `intent fulfil`; `intent driven`; `tensor program`; `tensor code`; `query refinement`; `index advis`; `systems design and optimi`; `systems research`; `operating system and artificial`; `generative file system` |

## Screening and Venue Criteria

Title and abstract screening applied the survey scope, with introductions consulted where needed. Duplicate
publications were merged by retaining the most complete version. Full-text review resolved uncertain eligibility
and the model's evaluated contribution.

The primary search population was restricted to CORE 2026 A*/A conferences, SJR 2025 Q1 journals, and six
proceedings journals associated with SIGMOD, FSE/ISSTA, CoNEXT, POPL/PLDI, SIGMETRICS, and VLDB. The latter
include Proceedings of the VLDB Endowment as well as Proceedings of the ACM titles. Preprints, workshops,
posters, demonstrations, magazines, and unranked venues were excluded from this primary population. Venue
assignments were resolved through DBLP where possible and otherwise through arXiv journal references,
Semantic Scholar, Crossref, or the publisher.

## Snowballing and Supplementary Search

Backward and forward snowballing used OpenAlex, starting from the 499 works retained after venue and eligibility
screening. Four rounds identified 60 additional works: 31 indexed in the snapshot but missed by the title query,
and 29 not yet indexed. These works underwent the subsequent selection stages listed below.

A separate supplementary search considered venue-excluded works whose author affiliations matched 36 major
industrial and frontier laboratories. It yielded 216 candidates, of which 46 were included
after eligibility review and coding. This route relaxes the venue restriction; it is not intended to provide
exhaustive or representative coverage of work outside the primary population.

## Selection Flow

The stages below reproduce the primary selection flow reported in the paper. Counts are retained works unless
otherwise indicated; title-query counts precede duplicate merging.

| Stage and count |
|---|
| DBLP snapshot, 1 Sep 2026: 2,414,509 records searched |
| Title query: 81,132 records, 69,456 unique titles |
| Title screening: 2,962 |
| Abstract and introduction screening, duplicate merging: 2,165 |
| Venue and eligibility screening: 499 |
| Snowballing (+60): 559 |
| Non-regular publications (-43): 516 |
| Full-text eligibility review (-49): 467 |
| Scope refinement (-163): 304 |

The primary flow yields 304 works. Adding 46 supplementary works
produces the final 350 works, comprising 317 archetype studies and 33 benchmark or evaluation
studies. Each work appears once in the final corpus.
