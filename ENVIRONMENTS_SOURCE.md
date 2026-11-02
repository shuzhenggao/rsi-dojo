# RSI-Dojo Environment Sources

This document lists the benchmark provenance and runtime requirements for the
released RSI-Dojo environments. The source table is generated from the
normalized task metadata under `src/eval/tasks/open-rsi` in the release
workspace.

Each row corresponds to one executable environment. `Source type` indicates whether the environment was derived from an InspectAI task or from a paper / public dataset source. `Source` records the normalized source description used by the environment metadata.

Total environments: **281**

| Source type | Count |
|---|---:|
| Paper / dataset | 212 |
| InspectAI | 69 |

## Runtime Environment

The local runner loads `local_env.sh`, prepares an isolated job directory, and
then installs the per-job Python environment used by the agent. In the `run1.sh`
execution path, dependency installation happens in `src/run_task.sh` through:

```bash
python -m pip install --user -r requirements.txt
```

Some environments use an LLM judge during evaluation. Before launching those
runs, configure the judge endpoint in the shell:

```bash
export EVAL_OPENAI_AK=...
export EVAL_OPENAI_ENDPOINT=...
```

Core runtime packages:

| Package | Version / constraint |
|---|---|
| `datasets` | `==4.5.0` |
| `transformers` | `==4.57.3` |
| `huggingface-hub` | `==0.36.0` |
| `httpx` | `>=0.27,<1` |
| `inspect-ai` | `==0.3.179` |
| `inspect-evals` | `==0.3.106` with `fortress`, `math`, `medqa`, `personality`, `sciknoweval`, and `worldsense` extras |
| `torch` | `==2.8.0` |
| `vllm` | `==0.11.0` |

Additional benchmark dependencies installed by the runner:

`accelerate`, `bert-score`, `cloudpickle`, `evaluate`, `fcd`, `jieba`,
`jinja2`, `jsonlines`, `jq`, `langchain-core`, `langdetect`,
`latex2sympy2-extended`, `math-verify==0.1.0`, `networkx`, `nltk`, `numpy`,
`openai`, `openpyxl`, `pandas`, `pebble`, `pint`, `protobuf`, `psutil`,
`pyarrow`, `pypinyin`, `python-dateutil`, `python-Levenshtein`, `PyYAML`,
`rdkit`, `requests`, `rouge`, `rouge-score`, `sacrebleu`, `scikit-learn`,
`scipy`, `sentence-transformers`, `sentencepiece`, `sympy`,
`timeout-decorator`, `torchmetrics`, `tqdm`, `unified-planning`, and `xlrd`.

The runner uses a local implementation for IFEval-style tasks, so the optional
`instruction-following-eval` GitHub dependency is not installed by default.

## Sources by Domain

### Math and Reasoning

45 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `agie_aqua_rat` | AGIEval Aqua-RAT | InspectAI | Inspect Evals AGIEval agie_aqua_rat | 254 | accuracy |
| `agie_logiqa_en` | AGIEval LogiQA English | InspectAI | Inspect Evals AGIEval agie_logiqa_en | 300 | accuracy |
| `agie_lsat_ar` | AGIEval LSAT-AR | InspectAI | Inspect Evals AGIEval agie_lsat_ar | 230 | accuracy |
| `agie_lsat_lr` | AGIEval LSAT-LR | InspectAI | Inspect Evals AGIEval agie_lsat_lr | 300 | accuracy |
| `agie_lsat_rc` | AGIEval LSAT-RC | InspectAI | AGIEval LSAT-RC frozen InspectAI samples | 269 | accuracy |
| `agie_sat_math` | AGIEval SAT Math | InspectAI | AGIEval SAT Math frozen InspectAI samples | 220 | accuracy |
| `aime2024` | AIME 2024 | InspectAI | AIME 2024 benchmark frozen InspectAI samples | 60 | accuracy |
| `all_that_glisters_is_not_gold_a_benchmark_for_reference_free_counterfactual_fina` | All That Glisters Is Not Gold | Paper / dataset | All That Glisters Is Not Gold benchmark frozen evaluated examples | 300 | positive_recall |
| `arc_challenge` | ARC Challenge | InspectAI | AI2 Reasoning Challenge ARC-Challenge frozen InspectAI samples | 300 | accuracy |
| `arc_easy` | ARC Easy | InspectAI | AI2 Reasoning Challenge ARC-Easy frozen InspectAI samples | 300 | accuracy |
| `bbeh` | BBEH | InspectAI | BBEH benchmark frozen samples | 300 | accuracy |
| `bbeh_mini` | BBEH Mini | InspectAI | Inspect Evals BBEH mini frozen samples | 300 | accuracy |
| `bbh` | BBH | InspectAI | BIG-Bench Hard frozen InspectAI samples | 300 | accuracy |
| `cogbench` | CogBench | Paper / dataset | CogBench TemporalDiscounting fixed procedural evaluation runs | 300 | means.performance_score1 |
| `dbqr_qa_a_question_answering_dataset_on_a_hybrid_of_database_querying_and_reason` | DBQR-QA: A Question Answering Dataset on a Hybrid of Database Querying and Reasoning | Paper / dataset | DBQR-QA public test split from the DBQR-QA benchmark | 150 | accuracy |
| `gpqa_diamond` | GPQA Diamond | InspectAI | GPQA Diamond benchmark frozen samples | 198 | accuracy |
| `gsm_plus_a_comprehensive_benchmark_for_evaluating_the_robustness_of_llm_s_as_mat` | GSM-Plus | Paper / dataset | GSM-Plus benchmark testmini examples | 300 | accuracy |
| `hardmath2` | HARDMath2 | Paper / dataset | HARDMath2 dataset from JVRoggeveen/HARDMath2 train split | 211 | pass_at_1 |
| `hardmath_a_benchmark_dataset_for_challenging_problems_in_applied_mathematics` | HARDMath: A Benchmark Dataset for Challenging Problems in Applied Mathematics | Paper / dataset | HARDMath benchmark public dataset from the HARDMath repository | 300 | average_score |
| `how_is_llm_reasoning_distracted_by_irrelevant_context_an_analysis_using_a_controlled_benchmark` | How Is LLM Reasoning Distracted by Irrelevant Context? An Analysis Using a Controlled Benchmark | Paper / dataset | GSM-DC Dataset Sample from Hugging Face dataset YMinglai/GSM-DC-Dataset-Sample | 300 | eacc |
| `i_f_qa_a_dataset_for_open_domain_question_answering_under_counterfactual_presupp` | IfQA: A Dataset for Open-domain Question Answering under Counterfactual Presuppositions | Paper / dataset | IfQA benchmark full_split test set | 300 | exact_match_f1 |
| `liar_liar_logical_mire` | Liar, Liar, Logical Mire | Paper / dataset | Liar, Liar, Logical Mire public generation recipe from the TruthQuest benchmark | 300 | accuracy |
| `llmthinkbench` | LLMThinkBench | Paper / dataset | LLMThinkBench official arithmetic and list reasoning datasets from the LLMThinkBench repository | 300 | overall_accuracy |
| `math` | MATH | InspectAI | MATH benchmark frozen InspectAI samples | 300 | accuracy |
| `mathador_lm` | Mathador-LM | Paper / dataset | Mathador-LM benchmark generated with official logic and fixed local evaluation samples | 300 | mean_normalized_score |
| `m_ath_b_ench_evaluating_the_theory_and_application_proficiency_of_llm_s_with_a_h` | MathBench | Paper / dataset | MathBench hierarchical mathematics benchmark | 300 | Overall |
| `matt` | MaTT | Paper / dataset | MaTT official data from the Mathematical Topic Tree benchmark | 300 | accuracy |
| `m_enat_qa_a_new_dataset_for_testing_the_temporal_comprehension_and_reasoning_abi` | MenatQA | Paper / dataset | MenatQA benchmark temporal question answering dataset | 300 | answer_f1 |
| `mgsm` | MGSM | InspectAI | MGSM benchmark frozen InspectAI samples | 300 | accuracy |
| `mmlu_cf` | MMLU - CF | Paper / dataset | MMLU-CF public validation data from microsoft/MMLU-CF | 300 | accuracy |
| `mmlu_0_shot` | MMLU 0-shot | InspectAI | MMLU benchmark frozen evaluated examples | 300 | accuracy |
| `mmlu_5_shot` | MMLU 5-shot | InspectAI | MMLU 5-shot frozen InspectAI samples | 300 | accuracy |
| `mmlu_pro` | MMLU-Pro | InspectAI | MMLU-Pro benchmark frozen samples | 300 | accuracy |
| `morables_a_benchmark_for_assessing_abstract_moral_reasoning_in_llm_s_with_fables` | Morables: A Benchmark for Assessing Abstract Moral Reasoning in LLMs with Fables | Paper / dataset | Morables benchmark frozen evaluated examples | 300 | accuracy |
| `neo_classic_a_benchmark_for_evaluating_linguistic_aesthetic_reasoning_in_classic` | Neo-Classic | Paper / dataset | NEO-CLASSIC benchmark tang.guess_author.standard evaluated examples | 300 | accuracy |
| `omni_math` | Omni-MATH | Paper / dataset | Omni-MATH-Rule official subset from the Omni-MATH benchmark | 300 | acc |
| `phun_bench_evaluating_llm_s_on_phonological_understanding_in_c_hinese` | Phun-Bench | Paper / dataset | Phun-Bench public phonological understanding benchmark | 300 | macro_task_score |
| `rpc_bench_a_fine_grained_benchmark_for_research_paper_comprehension` | RPC-Bench: A Fine-grained Benchmark for Research Paper Comprehension | Paper / dataset | RPC-Bench public benchmark frozen evaluated examples | 300 | overall_score |
| `street` | STREET | Paper / dataset | STREET benchmark frozen test examples from GSM8K, SCONE, and AQUA-RAT subsets | 300 | macro_answer_acc |
| `tau_bench` | tau-bench | Paper / dataset | sierra-research/tau-bench public benchmark | 165 | accuracy |
| `t_heorem_qa_a_theorem_driven_question_answering_dataset` | TheoremQA | Paper / dataset | TheoremQA theorem-driven question answering benchmark | 300 | accuracy |
| `t_imeline_qa_a_benchmark_for_question_answering_over_timelines` | Timeline QA : A Benchmark for Question Answering over Timelines | Paper / dataset | TimelineQA benchmark from facebookresearch/TimelineQA | 254 | accuracy |
| `utm_ath_a_benchmark_for_math_evaluation_with_unit_test` | UTMath: A Benchmark for Math Evaluation with Unit Test | Paper / dataset | UTMath benchmark fixed unit-test subset from UTMathGroup/UTMath | 300 | pass_at_1 |
| `w_ireless_m_ath_b_ench` | WirelessMathBench | Paper / dataset | XINLI1997/WirelessMathBench public benchmark data | 300 | overall_accuracy |
| `worldsense` | WorldSense | Paper / dataset | WorldSense test set from facebookresearch/worldsense | 300 | ws_accuracy |

### Code and Tool Use

4 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `apps` | APPS | InspectAI | codeparrot/apps frozen local samples | 300 | accuracy |
| `mbpp` | MBPP | InspectAI | MBPP sanitized test split frozen InspectAI samples | 257 | pass_at_1 |
| `s_ub_t_oken_t_est` | S ub T oken T est | Paper / dataset | Rain-air/SubTokenTest-QA public JSONL benchmark | 300 | overall_exact_match_rate |
| `toolace` | ToolACE | Paper / dataset | Team-ACE/ToolACE public data.json | 300 | exact_match |

### Science and Medicine

39 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `a_fri_m_ed_qa_a_pan_a_frican_multi_specialty_medical_question_answering_benchmar` | AfriMed-QA Pan-African Multi-Specialty Medical Question Answering Benchmark | Paper / dataset | AfriMed-QA public benchmark MCQ test split | 300 | accuracy |
| `anessuite_a_comprehensive_benchmark_and_dataset_suite_for_anesthesiology_reasoni` | AnesSuite: A Comprehensive Benchmark and Dataset Suite for Anesthesiology Reasoning in LLMs | Paper / dataset | AnesSuite anesthesiology multiple-choice reasoning benchmark frozen evaluated examples | 300 | accuracy |
| `atmossci_bench_evaluating_the_recent_advance_of_large_language_model_for_atmosph` | AtmosSci-Bench: Evaluating the Recent Advance of Large Language Model for Atmospheric Science | Paper / dataset | AtmosSci-Bench atmospheric science multiple-choice benchmark frozen evaluated examples | 300 | accuracy |
| `b_io_h_op_r` | BioHopR | Paper / dataset | BioHopR public benchmark data from knowlab-research/BioHopR | 300 | overall.precision_at_0.9 |
| `chembench` | ChemBench | InspectAI | ChemBench frozen InspectAI samples | 300 | accuracy |
| `c_hrono_b_ias_a_benchmark_for_evaluating_time_conditional_group_bias_in_the_time` | ChronoBias | Paper / dataset | tml-lab/ChronoBias train split | 300 | exact_match_accuracy |
| `cm_ed_c_alc_bench_a_fine_grained_benchmark_for_c_hinese_medical_calculations_in_` | CMedCalc-Bench | Paper / dataset | CMedCalc-Bench public benchmark data from Zhihong-Zhu/CMedCalc-Bench | 300 | accuracy |
| `cmphysbench_a_benchmark_for_evaluating_large_language_models_in_condensed_matter` | CMPhysBench: A Benchmark for Evaluating Large Language Models in Condensed Matter Physics | Paper / dataset | CMPhysBench condensed matter physics benchmark public dataset | 300 | P@1 SEED |
| `cmqcic_bench_a_c_hinese_benchmark_for_evaluating_large_language_models_in_medica` | CMQCIC-Bench: A Chinese Benchmark for Evaluating Large Language Models in Medical Quality Control Indicator Calculation | InspectAI | CMQCIC-Bench frozen seeded random sample | 300 | accuracy |
| `diagnosisarena` | DiagnosisArena | Paper / dataset | DiagnosisArena public MCQ test split from SII-SPIRAL-MED/DiagnosisArena | 300 | accuracy |
| `d_isast_qa_a_comprehensive_benchmark_for_evaluating_question_answering_in_disast` | DisastQA: A Comprehensive Benchmark for Evaluating Question Answering in Disaster Management | Paper / dataset | DisastQA benchmark multiple-choice QA frozen evaluated examples | 300 | overall_accuracy |
| `frontierscience` | Frontierscience | InspectAI | Frontierscience frozen InspectAI samples | 160 | accuracy |
| `genomeqa` | GenomeQA | Paper / dataset | GenomeQA public benchmark data | 300 | accuracy |
| `holistic_reasoning_with_long_context_lms` | Holistic Reasoning with Long-Context LMs | Paper / dataset | HoloBench official dataset megagonlabs/holobench localized frozen examples | 86 | relaxed_row_recall |
| `lab_bench_dbqa` | Lab Bench DBQA | InspectAI | Lab Bench DBQA frozen InspectAI samples | 300 | precision |
| `lab_bench_litqa` | Lab Bench LitQA | InspectAI | Lab Bench LitQA benchmark frozen InspectAI samples | 199 | accuracy |
| `lab_bench_protocolqa` | Lab Bench ProtocolQA | InspectAI | Lab Bench ProtocolQA frozen InspectAI samples | 108 | precision |
| `lab_bench_seqqa` | Lab Bench SeqQA | InspectAI | Lab Bench SeqQA benchmark frozen InspectAI samples | 300 | accuracy |
| `lab_bench_cloning_scenarios` | LAB-Bench Cloning Scenarios | InspectAI | LAB-Bench Cloning Scenarios frozen InspectAI samples | 50 | accuracy |
| `lab_bench_suppqa` | LAB-Bench SuppQA | InspectAI | LAB-Bench SuppQA frozen samples | 82 | accuracy |
| `m_arena_hard` | m-ArenaHard | Paper / dataset | CohereLabs m-ArenaHard multilingual prompt benchmark with local Qwen3 baseline answers | 300 | win_rate |
| `m_qalm_a_benchmark_to_assess_clinical_reading_comprehension_and_knowledge_recall` | M-QALM: A Benchmark to Assess Clinical Reading Comprehension and Knowledge Recall | Paper / dataset | M-QALM benchmark fixed clinical multiple-choice question answering sample | 300 | accuracy |
| `macaron` | Macaron | Paper / dataset | Macaron public benchmark data from AlaaAhmed2444/Macaron | 300 | accuracy |
| `measuring_risk_of_bias_in_biomedical_reports` | Measuring Risk of Bias in Biomedical Reports | Paper / dataset | RoBBR benchmark main task Cochrane and non-Cochrane frozen test samples | 100 | macro_f1 |
| `medarabench_large_scale_arabic_medical_question_answering_dataset_and_benchmark` | MedAraBench: Large-scale Arabic Medical Question Answering Dataset and Benchmark | Paper / dataset | MedAraBench large-scale Arabic medical question answering benchmark test split | 300 | accuracy |
| `medcalc_bench_evaluating_large_language_models_for_medical_calculations` | MedCalc-Bench | Paper / dataset | MedCalc-Bench medical calculation benchmark evaluated examples | 300 | overall_accuracy |
| `medec_a_benchmark_for_medical_error_detection_and_correction_in_clinical_notes` | MEDEC: A Benchmark for Medical Error Detection and Correction in Clinical Notes | Paper / dataset | MEDEC public labeled MEDEC-MS test subset with deterministic frozen sample | 300 | R1FC |
| `m_ed_e_rr_b_ench_a_fine_grained_multilingual_benchmark_for_medical_error_detecti` | MedErrBench | Paper / dataset | MedErrBench fine-grained multilingual benchmark for medical error detection | 300 | accuracy |
| `m_ed_f_act_a_large_scale_c_hinese_dataset_for_evidence_based_medical_fact_checki` | MedFact: A Large-scale Chinese Dataset for Evidence-based Medical Fact Checking | Paper / dataset | MedFact public training data fixed claim-level evaluation sample | 300 | macro_f1 |
| `m_ed_h_allu_a_comprehensive_benchmark_for_detecting_medical_hallucinations_in_la` | MedHallu: A Comprehensive Benchmark for Detecting Medical Hallucinations in Large Language Models | Paper / dataset | MedHallu benchmark frozen evaluated examples | 300 | with_knowledge_f1 |
| `medqa` | MedQA | InspectAI | MedQA benchmark frozen samples | 300 | accuracy |
| `meqa_a_benchmark_for_multi_hop_event_centric_question_answering_with_explanation` | MEQA: A Benchmark for Multi-hop Event-centric Question Answering with Explanations | Paper / dataset | MEQA benchmark public data from du-nlp-lab/MEQA | 288 | answer_f1 |
| `neoqa` | NeoQA | Paper / dataset | NeoQA public benchmark test split from the official Amazon Science NeoQA repository | 300 | adt_score |
| `pubmedqa` | PubMedQA | InspectAI | PubMedQA frozen InspectAI samples | 300 | accuracy |
| `s_eed_b_ench_a_multi_task_benchmark_for_evaluating_large_language_models_in_seed` | SeedBench | Paper / dataset | SeedBench zero-shot benchmark examples from the InternScience SeedBench repository | 300 | task_macro_average |
| `s_yllabus_qa_a_course_logistics_question_answering_dataset` | SyllabusQA: A Course Logistics Question Answering Dataset | Paper / dataset | SyllabusQA public course logistics question answering benchmark test split | 300 | f1 |
| `wmdp_bio` | WMDP Biology | Paper / dataset | WMDP Biology multiple-choice benchmark frozen samples | 300 | accuracy |
| `wmdp_chem` | WMDP Chemistry | InspectAI | WMDP Chemistry frozen InspectAI samples | 300 | accuracy |
| `yokaieval` | YokaiEval | Paper / dataset | CyberAgentAILab YokaiEval benchmark dataset | 300 | accuracy |

### Safety and Robustness

17 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `ctibench_a_benchmark_for_evaluating_llms_in_cyber_threat_intelligence` | CTIBench: A Benchmark for Evaluating LLMs in Cyber Threat Intelligence | Paper / dataset | CTIBench public cyber threat intelligence benchmark MCQ subset | 300 | mcq_accuracy |
| `detection_and_positive_reconstruction_of_cognitive_distortion_sentences_m_andari` | Detection and Positive Reconstruction of Cognitive Distortion Sentences: Mandarin Dataset and Evaluation | Paper / dataset | Detection and Positive Reconstruction of Cognitive Distortion Sentences Mandarin benchmark frozen evaluated examples | 300 | accuracy |
| `drpbench` | DRPBench | Paper / dataset | DRPBench official benchmark payload from the public DRPBench repository | 300 | data_race_detection_and_localization |
| `d_yna_q_uest_a_dynamic_question_answering_dataset_reflecting_real_world_knowledg` | DynaQuest: A Dynamic Question Answering Dataset Reflecting Real-World Knowledge Updates | Paper / dataset | DynaQuest benchmark frozen evaluated examples | 300 | f1 |
| `factify_5wqa` | FACTIFY-5WQA | Paper / dataset | FACTIFY-5WQA benchmark frozen evaluated examples | 300 | accuracy |
| `flex` | FLEX | Paper / dataset | FLEX fairness robustness benchmark combined official test CSVs | 300 | accuracy |
| `flexbench` | FlexBench | Paper / dataset | FlexBench public moderation benchmark test data from the FlexGuard project | 300 | severity_accuracy |
| `g_uard_b_ench` | GuardBench | Paper / dataset | GuardBench OpenAI Moderation Dataset formatted frozen examples | 300 | f1 |
| `indibias` | IndiBias | Paper / dataset | IndiBias public sample data from the IndiBias benchmark | 300 | accuracy |
| `safetybench` | SafetyBench | Paper / dataset | SafetyBench public benchmark data | 300 | accuracy |
| `s_cholar_b_ench_a_bilingual_benchmark_for_abstraction_comprehension_and_reasonin` | ScholarBench: A Bilingual Benchmark for Abstraction, Comprehension, and Reasoning Evaluation in Academic Contexts | Paper / dataset | KISTI-KONI ScholarBench bilingual academic abstraction, comprehension, and reasoning benchmark | 300 | overall_core_macro |
| `stereoset` | StereoSet | InspectAI | StereoSet benchmark frozen local samples | 300 | stereotype_score |
| `strong_reject` | StrongREJECT | InspectAI | StrongREJECT benchmark frozen InspectAI samples | 300 | strong_reject_score |
| `sycobench` | SycoBench-600 | Paper / dataset | SycoBench-600 public benchmark from debu-sinha/sycobench-600 | 300 | sycophancy_and_correction_selectivity |
| `sycophancy` | Sycophancy | InspectAI | Anthropic sycophancy are-you-sure benchmark frozen local samples | 300 | truthfulness |
| `the_sif_o_benchmark` | The SIFo Benchmark | Paper / dataset | The SIFo Benchmark official QA, math, security, and text modification benchmark files from the SIFo repository | 300 | instruction_acc |
| `wmdp_cyber` | WMDP Cyber | InspectAI | WMDP Cyber benchmark data from Inspect Evals wmdp_cyber | 300 | accuracy |

### Finance, Legal, and Professional

13 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `alphabench` | AlphaBench | Paper / dataset | AlphaBench CSI300 T4 pairwise-select test split | 90 | pairwise_accuracy |
| `benchmarking_large_language_models_on_cflue_a_c_hinese_financial_language_unders` | CFLUE Knowledge | Paper / dataset | CFLUE Chinese financial language understanding benchmark knowledge subset from the public cflue repository | 300 | accuracy |
| `developing_a_pragmatic_benchmark_for_assessing_k_orean_legal_language_understanding_in_large_language_models` | Developing a Pragmatic Benchmark for Assessing Korean Legal Language Understanding in Large Language Models | Paper / dataset | KBL Korean legal language understanding benchmark public closed-book examples from lbox/kbl | 300 | overall_accuracy |
| `edinet_bench_evaluating_llms_on_complex_financial_tasks_using_japanese_financial` | EDINET-Bench: Evaluating LLMs on Complex Financial Tasks using Japanese Financial Statements | Paper / dataset | EDINET-Bench public benchmark from SakanaAI evaluating Japanese financial statement tasks | 300 | macro_accuracy_all |
| `f_in_t_rust_a_comprehensive_benchmark_of_trustworthiness_evaluation_in_finance_d` | FinTrust: A Comprehensive Benchmark of Trustworthiness Evaluation in Finance Domain | Paper / dataset | FinTrust benchmark frozen evaluated examples | 100 | accuracy |
| `golden_touchstone_a_comprehensive_bilingual_benchmark_for_evaluating_financial_l` | Golden-Touchstone | Paper / dataset | Golden-Touchstone comprehensive bilingual financial benchmark frozen evaluated examples | 300 | average_result |
| `l_ex_g_enius` | LexGenius | Paper / dataset | LexGenius benchmark public multiple-choice legal general intelligence questions | 300 | overall_accuracy |
| `legalbench` | LegalBench | Paper / dataset | LegalBench public benchmark frozen auto-scored examples | 289 | macro_balanced_accuracy |
| `lexeval_a_comprehensive_chinese_legal_benchmark_for_evaluating_large_language_mo` | LexEval: A Comprehensive Chinese Legal Benchmark for Evaluating Large Language Models | Paper / dataset | CSHaitao/LexEval official Hugging Face dataset bring-up subset | 100 | overall_exact_match |
| `o_pen_e_xempt_a_diagnostic_benchmark_for_legal_reasoning_and_a_framework_for_cre` | OpenExempt | Paper / dataset | OpenExempt baseline robustness benchmark fixed test examples | 300 | example_weighted_f1 |
| `phantom_a_benchmark_for_hallucination_detection_in_financial_long_context_qa` | PHANTOM: A Benchmark for Hallucination Detection in Financial Long-Context QA | Paper / dataset | PHANTOM Hallucination Detection benchmark financial long-context QA examples | 300 | accuracy |
| `p_riva_ci_bench_evaluating_privacy_with_contextual_integrity_and_legal_complianc` | PrivaCI-Bench: Evaluating Privacy with Contextual Integrity and Legal Compliance | Paper / dataset | HKUST-KnowComp PrivaCI-Bench official MCQ_list_try_hard split | 102 | accuracy |
| `s_wi_lt_ra_bench_the_s_wiss_legal_translation_benchmark` | Swiss Legal Translation Benchmark | Paper / dataset | Swiss Legal Translation Benchmark frozen evaluated examples | 300 | chrf2pp |

### Multilingual and Culture

62 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `arabic_safeguard` | Arabic Dataset for LLM Safeguard Evaluation | Paper / dataset | Arabic_safety_evaluation public Arabic safeguard evaluation data | 300 | accuracy |
| `batayan_a_f_ilipino_nlp_benchmark_for_evaluating_large_language_models` | Batayan: A Filipino NLP Benchmark for Evaluating Large Language Models | Paper / dataset | Batayan Filipino NLP benchmark TL-PAWS paraphrase examples | 300 | accuracy |
| `be_n_qa_a_question_answering_benchmark_for_b_engali_and_e_nglish` | BEnQA | Paper / dataset | BEnQA question answering benchmark for Bengali and English frozen evaluated examples | 300 | accuracy |
| `bertaqa` | BertaQA | Paper / dataset | BertaQA English and Basque benchmark test splits from the BertaQA dataset | 300 | accuracy |
| `blend_a_benchmark_for_llms_on_everyday_knowledge_in_diverse_cultures_and_languag` | BLEnD: A Benchmark for LLMs on Everyday Knowledge in Diverse Cultures and Languages | Paper / dataset | BLEnD multiple-choice everyday cultural knowledge benchmark frozen evaluated examples | 300 | accuracy |
| `c_on_l_oan_a_contrastive_multilingual_dataset_for_evaluating_loanwords` | ConLoan: A Contrastive Multilingual Dataset for Evaluating Loanwords | Paper / dataset | ConLoan public contrastive loanword dataset | 300 | contrastive_accuracy |
| `c_x_mp_a_linguistic_minimal_pair_benchmark_for_evaluating_constructional_underst` | CxMP: A Linguistic Minimal-Pair Benchmark for Evaluating Constructional Understanding in Language Models | Paper / dataset | CxMP benchmark frozen evaluated examples from the CxMP constructional minimal-pair dataset | 300 | accuracy_semantic_valid |
| `cce_val_a_representative_evaluation_benchmark_for_the_c_hinese_centric_multiling` | CCEval Chinese-Centric Multilingual Evaluation Benchmark | Paper / dataset | CCEval public validation examples with frozen local proxy references | 300 | chrf |
| `ceb_compositional_evaluation_benchmark_for_fairness_in_large_language_models` | CEB Compositional Evaluation Benchmark for Fairness in Large Language Models | Paper / dataset | Compositional Evaluation Benchmark for Fairness in Large Language Models public benchmark data | 300 | accuracy |
| `c_hinese_s_afety_qa_a_safety_short_form_factuality_benchmark_for_large_language_` | Chinese SafetyQA | Paper / dataset | Chinese SafetyQA benchmark frozen evaluated examples | 300 | accuracy |
| `cif_bench_a_c_hinese_instruction_following_benchmark_for_evaluating_the_generali` | CIF-Bench: A Chinese Instruction-Following Benchmark for Evaluating the Generalizability of Large Language Models | Paper / dataset | CIF-Bench benchmark frozen evaluated examples | 300 | overall_score |
| `cl_ong_e_val_a_c_hinese_benchmark_for_evaluating_long_context_large_language_mod` | CLongEval Chinese Benchmark for Evaluating Long-Context Large Language Models | Paper / dataset | CLongEval small split frozen evaluated examples | 300 | macro_small_score |
| `cmhg_a_dataset_and_benchmark_for_headline_generation_of_minority_languages_in_c_` | CMHG: A Dataset and Benchmark for Headline Generation of Minority Languages in China | Paper / dataset | KEVVVV/CMHG high-quality annotated headline generation subsets for Tibetan, Traditional Mongolian, and Uyghur | 300 | rouge_l_f1 |
| `cm_oral_e_val_a_moral_evaluation_benchmark_for_c_hinese_large_language_models` | CMoralEval: A Moral Evaluation Benchmark for Chinese Large Language Models | Paper / dataset | CMoralEval public benchmark test split | 300 | accuracy |
| `cotempqa` | CoTempQA | Paper / dataset | CoTempQA benchmark from Living in the Moment: Can Large Language Models Grasp Co-Temporal Reasoning? | 300 | overall_accuracy_f1_average |
| `cr_isk_e_val_a_c_hinese_multi_level_risk_evaluation_benchmark_dataset_for_large_` | CRiskEval | Paper / dataset | CRiskEval Chinese multi-level risk evaluation benchmark | 300 | accuracy |
| `c_ultural_b_ench_a_robust_diverse_and_challenging_benchmark_for_measuring_lm_s_c` | CulturalBench | Paper / dataset | CulturalBench benchmark frozen evaluated examples | 300 | accuracy |
| `e_eval_a_comprehensive_c_hinese_k_12_education_evaluation_benchmark_for_large_la` | E-EVAL: A Comprehensive Chinese K-12 Education Evaluation Benchmark for Large Language Models | Paper / dataset | E-EVAL Chinese K-12 education benchmark validation split | 300 | accuracy |
| `e_mo_b_ench_ua_a_benchmark_dataset_for_emotion_detection_in_u_krainian` | EmoBench-UA | Paper / dataset | EmoBench-UA benchmark frozen evaluated examples from the public Ukrainian emotion detection dataset | 300 | macro_f1 |
| `e_ngi_b_ench_a_benchmark_for_evaluating_large_language_models_on_engineering_pro` | EngiBench | Paper / dataset | EngiBench public benchmark frozen evaluated examples | 300 | objective_slice_accuracy |
| `episodic_memories_generation_and_evaluation_benchmark_for_large_language_models` | Episodic Memories Generation and Evaluation Benchmark for Large Language Models | Paper / dataset | Episodic Memories Generation and Evaluation Benchmark frozen evaluated examples | 114 | episodic_memory_score |
| `etrqa_a_comprehensive_benchmark_for_evaluating_event_temporal_reasoning_abilitie` | ETRQA: A Comprehensive Benchmark for Evaluating Event Temporal Reasoning Abilities of Large Language Models | Paper / dataset | ETRQA benchmark frozen evaluated examples | 300 | accuracy |
| `evergreenqa` | EverGreenQA | Paper / dataset | EverGreenQA multilingual temporal question classification dataset from s-nlp/Evergreen-classification and s-nlp/EverGreen-Multilingual | 300 | accuracy |
| `g_reek_mmlu_a_native_sourced_multitask_benchmark_for_evaluating_language_models_` | GreekMMLU | Paper / dataset | GreekMMLU native-sourced multitask benchmark test split | 300 | accuracy |
| `h_alu_e_val_a_large_scale_hallucination_evaluation_benchmark_for_large_language_` | HaluEval | Paper / dataset | HaluEval benchmark frozen evaluated examples | 300 | overall_accuracy |
| `h_e_q_a_large_and_diverse_h_ebrew_reading_comprehension_benchmark` | HeQ: Large and Diverse Hebrew Reading Comprehension Benchmark | Paper / dataset | Etelis/HeQ_v1 validation split frozen evaluated examples | 300 | exact_match_and_f1 |
| `hi_t_o_m_a_benchmark_for_evaluating_higher_order_theory_of_mind_reasoning_in_lar` | Hi-ToM: A Benchmark for Evaluating Higher-Order Theory of Mind Reasoning in Large Language Models | Paper / dataset | Hi-ToM benchmark frozen evaluated examples | 300 | accuracy |
| `large_language_models_expert_level_global_history_knowledge_benchmark_hist_llm` | HiST-LLM | Paper / dataset | Large Language Models Expert-Level Global History Knowledge Benchmark HiST-LLM frozen evaluated examples | 300 | accuracy |
| `indic_qa` | IndicQA Hindi Extractive QA | Paper / dataset | IndicQA Benchmark Hindi extractive question answering subset from the public IndicQA dataset | 300 | exact_match |
| `i_ntention_qa_a_benchmark_for_evaluating_purchase_intention_comprehension_abilit` | IntentionQA: A Benchmark for Evaluating Purchase Intention Comprehension Abilities of Language Models in E-commerce | Paper / dataset | IntentionQA benchmark frozen evaluated examples | 300 | overall_accuracy |
| `jqbench_a_benchmark_for_reading_and_editing_json_from_natural_language_and_or_ex` | JQBench | Paper / dataset | DominuZ/jq-bench JQBench examples | 60 | accuracy |
| `ke_mhisto_towards_a_multilingual_historical_knowledge_extraction_benchmark_for_a` | KE-MHISTO DynaKnowledge QA | Paper / dataset | KE-MHISTO multilingual historical music knowledge benchmark DynaKnowledge datasets | 300 | soft_accuracy |
| `lexicon_a_benchmark_for_planning_under_temporal_constraints_in_natural_language` | LexiCon: a Benchmark for Planning under Temporal Constraints in Natural Language | Paper / dataset | LexiCon benchmark frozen evaluated examples from the public LexiCon benchmarks dataset | 88 | optimal_rate |
| `lingoly_a_benchmark_of_olympiad_level_linguistic_reasoning_puzzles_in_low_resour` | LINGOLY: A Benchmark of Olympiad-Level Linguistic Reasoning Puzzles in Low-Resource and Extinct Languages | Paper / dataset | LINGOLY benchmark evaluation data | 204 | exact_match_bleu_rouge1_chrf |
| `linguini_a_benchmark_for_language_agnostic_linguistic_reasoning` | Linguini: A benchmark for language-agnostic linguistic reasoning | Paper / dataset | Linguini benchmark frozen evaluation examples | 160 | item_accuracy |
| `m_c_be_a_multi_task_c_hinese_bias_evaluation_benchmark_for_large_language_models` | McBE: A Multi-task Chinese Bias Evaluation Benchmark for Large Language Models | Paper / dataset | McBE benchmark frozen evaluated examples | 300 | objective_avg |
| `m_i_tt_en_s_a_dataset_for_evaluating_gender_mistranslation` | MiTTenS: A Dataset for Evaluating Gender Mistranslation | Paper / dataset | MiTTenS public dataset test split translation-to-English examples | 300 | gender_accuracy |
| `mmath` | MMATH | Paper / dataset | MMATH multilingual mathematical reasoning benchmark from RUCAIBox/MMATH | 300 | pass_at_n_accuracy |
| `mmlu_pro_a_more_robust_and_challenging_multi_task_language_understanding_benchma` | MMLU-Pro: A More Robust and Challenging Multi-Task Language Understanding Benchmark | Paper / dataset | MMLU-Pro benchmark frozen evaluated examples | 300 | accuracy |
| `mmlu_p_ro_x_a_multilingual_benchmark_for_advanced_large_language_model_evaluatio` | MMLU-ProX: A Multilingual Benchmark for Advanced Large Language Model Evaluation | Paper / dataset | MMLU-ProX multilingual benchmark frozen evaluated examples | 300 | accuracy |
| `m_orpho_b_ench` | MorphoBench | Paper / dataset | OpenDCAI/MorphoBench text-only reasoning subsets | 300 | accuracy |
| `morphogen_a_multilingual_benchmark_for_evaluating_gender_aware_morphological_gen` | MORPHOGEN: A Multilingual Benchmark for Evaluating Gender-Aware Morphological Generation | Paper / dataset | MORPHOGEN ag2003/morphogen benchmark fixed sampled test records | 300 | Agg_Acc_micro |
| `mr_gsm8k_a_meta_reasoning_benchmark_for_large_language_model_evaluation` | MR-GSM8K: A Meta-Reasoning Benchmark for Large Language Model Evaluation | Paper / dataset | MR-GSM8K public benchmark data | 300 | mr_score_local |
| `n_or_e_val_a_n_orwegian_language_understanding_and_generation_evaluation_benchma` | NorEval: A Norwegian Language Understanding and Generation Evaluation Benchmark | Paper / dataset | NorEval benchmark frozen evaluated examples | 300 | weighted_acc |
| `neo_bench_evaluating_robustness_of_large_language_models_with_neologisms` | NEO-BENCH | Paper / dataset | NEO-BENCH benchmark Inputs.xlsx frozen evaluated examples | 300 | overall_accuracy |
| `or_bench_an_over_refusal_benchmark_for_large_language_models` | OR-Bench: An Over-Refusal Benchmark for Large Language Models | Paper / dataset | OR-Bench released hard and toxic prompt sets from bench-llm/or-bench | 300 | balanced_accuracy |
| `p_ak_bbq_a_culturally_adapted_bias_benchmark_for_qa` | PakBBQ: A Culturally Adapted Bias Benchmark for QA | Paper / dataset | PakBBQ culturally adapted bias benchmark for question answering | 300 | accuracy |
| `paradise_evaluating_implicit_planning_skills_of_language_models_with_procedural_` | PARADISE | Paper / dataset | PARADISE procedural warnings and tips benchmark test split | 300 | accuracy |
| `question_answering_in_a_low_resourced_language_benchmark_dataset_and_models_for_` | Question-Answering in a Low-resourced Language: Benchmark Dataset and Models for Tigrinya | Paper / dataset | TiQuAD Tigrinya question-answering benchmark frozen evaluated examples | 300 | f1 |
| `realmath_a_continuous_benchmark_for_evaluating_language_models_on_research_level` | RealMath: A Continuous Benchmark for Evaluating Language Models on Research-Level Mathematics | Paper / dataset | RealMath benchmark frozen evaluated examples from Math StackExchange | 300 | accuracy |
| `r_e_t_race_qa_evaluating_reasoning_traces_of_small_language_models_in_commonsens` | ReTraceQA | Paper / dataset | ReTraceQA evaluated commonsense question answering examples | 300 | accuracy |
| `sevenllm_mcq_zh` | SEvenLLM Chinese MCQ | InspectAI | SEvenLLM Chinese multiple-choice frozen samples | 50 | accuracy |
| `sevenllm_qa_zh` | SEvenLLM Chinese QA | InspectAI | SEvenLLM-Dataset local frozen Chinese QA samples | 300 | rouge_l_and_semantic_similarity |
| `steer_bench_a_benchmark_for_evaluating_the_steerability_of_large_language_models` | STEER-BENCH: A Benchmark for Evaluating the Steerability of Large Language Models | Paper / dataset | STEER-BENCH frozen evaluated multiple-choice examples | 300 | accuracy |
| `the_belebele_benchmark_a_parallel_reading_comprehension_dataset_in_122_language_` | The Belebele Benchmark: a Parallel Reading Comprehension Dataset in 122 Language Variants | Paper / dataset | Facebook Belebele benchmark frozen reading-comprehension examples | 300 | accuracy |
| `the_g_ao_y_ao_benchmark_a_comprehensive_framework_for_evaluating_multilingual_an` | The GaoYao Benchmark | Paper / dataset | The GaoYao Benchmark multilingual and multicultural benchmark frozen evaluated examples | 300 | macro_average |
| `the_music_maestro_or_the_musically_challenged_a_massive_music_evaluation_benchma` | The Music Maestro or The Musically Challenged, A Massive Music Evaluation Benchmark for Large Language Models | Paper / dataset | ZIQI-Eval music benchmark frozen evaluated examples | 300 | accuracy |
| `this_is_not_a_dataset_a_large_negation_benchmark_to_challenge_large_language_mod` | This is not a Dataset: A Large Negation Benchmark to Challenge Large Language Models | Paper / dataset | This is not a Dataset public negation benchmark evaluated examples | 300 | all.accuracy |
| `tlue_a_t_ibetan_language_understanding_evaluation_benchmark` | TLUE: A Tibetan Language Understanding Evaluation Benchmark | Paper / dataset | TLUE Ti-MMLU subset frozen evaluated examples | 300 | accuracy |
| `towards_robust_temporal_reasoning_of_large_language_models_via_a_multi_hop_qa_da` | Towards Robust Temporal Reasoning of Large Language Models via a Multi-hop QA Dataset | Paper / dataset | Complex-TR temporal multi-hop QA benchmark gold test examples | 300 | exact_match |
| `wenmind_a_comprehensive_benchmark_for_evaluating_large_language_models_in_chines` | WenMind | Paper / dataset | WenMind benchmark closed-form MCQ and fill-in-the-blank examples | 300 | accuracy |
| `when_llms_meet_cunning_texts_a_fallacy_understanding_benchmark_for_large_languag` | When LLMs Meet Cunning Texts: A Fallacy Understanding Benchmark for Large Language Models | Paper / dataset | When LLMs Meet Cunning Texts / FLUB benchmark frozen evaluated examples | 300 | accuracy |

### Long-context, Memory, and QA

35 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `advqa` | AdvQA | Paper / dataset | AdvScore official AdvQA data/Advqa_text.csv | 182 | exact_match |
| `boolq` | BoolQ | InspectAI | BoolQ validation frozen InspectAI samples | 300 | accuracy |
| `chartom_qa` | CharToM-QA | Paper / dataset | CharToM-QA benchmark frozen evaluated examples | 300 | accuracy |
| `commonsense_qa` | CommonsenseQA | InspectAI | tau/commonsense_qa validation split via InspectAI commonsense_qa | 300 | accuracy |
| `c_omplex_t_emp_qa_a_100m_dataset_for_complex_temporal_question_answering` | ComplexTempQA 100M | Paper / dataset | ComplexTempQA 100M benchmark frozen evaluated examples | 200 | exact_match |
| `c_ond_a_mbig_qa_a_benchmark_and_dataset_for_conditional_ambiguous_question_answe` | CondAmbigQA: A Benchmark and Dataset for Conditional Ambiguous Question Answering | Paper / dataset | CondAmbigQA benchmark frozen evaluated examples | 300 | average_balanced_score |
| `drop` | DROP | InspectAI | DROP frozen InspectAI samples | 300 | f1 |
| `e_volve_b_ench_a_comprehensive_benchmark_for_assessing_temporal_awareness_in_llm` | EvolveBench | Paper / dataset | EvolveBench frozen evaluated examples for temporal awareness assessment | 300 | overall_accuracy |
| `finlfqa` | FinLFQA | Paper / dataset | Dragongon/FinLFQA validation and test splits | 300 | answer_rougeL |
| `ifir` | IFIR | Paper / dataset | IFIR FIQA test data | 300 | micro_f1 |
| `k_o_rc_knowledge_oriented_reading_comprehension_benchmark_for_deep_text_understa` | KoRC: Knowledge Oriented Reading Comprehension Benchmark for Deep Text Understanding | Paper / dataset | KoRC benchmark frozen evaluated examples | 300 | em_acc_with_penalty |
| `lc_eval_a_bilingual_multi_task_evaluation_benchmark_for_long_context_understandi` | LC-Eval: A Bilingual Multi-Task Evaluation Benchmark for Long Context Understanding | Paper / dataset | humain-ai/LC-Eval bilingual multi-task long-context evaluation dataset | 300 | score |
| `m_4_le_a_multi_ability_multi_range_multi_task_multi_domain_long_context_evaluati` | M4LE | Paper / dataset | M4LE public benchmark from the wckwan/M4LE dataset | 300 | accuracy |
| `mintqa_a_multi_hop_question_answering_benchmark_for_evaluating_llm_s_on_new_and_` | MINTQA: A Multi-Hop Question Answering Benchmark for Evaluating LLMs on New and Long-tail Knowledge | Paper / dataset | MINTQA multi-hop question answering benchmark public POP and TI examples | 300 | accuracy |
| `narrowing_the_knowledge_evaluation_gap_open_domain_question_answering_with_multi` | Narrowing the Knowledge Evaluation Gap: Open-Domain Question Answering with Multi-Granularity Answers | Paper / dataset | GRANOLA entity questions from the Narrowing the Knowledge Evaluation Gap benchmark | 300 | granola_accuracy |
| `novelhopqa` | NovelHopQA | Paper / dataset | NovelHopQA public Hugging Face dataset frozen evaluated examples | 300 | exact_match_and_token_f1 |
| `perturbqa` | PerturbQA | Paper / dataset | PerturbQA official benchmark data from the Genentech PerturbQA repository | 300 | classification_accuracy |
| `piqa` | PIQA | InspectAI | Inspect Evals PIQA frozen samples | 300 | accuracy |
| `qadynamics_training_dynamics_driven_synthetic_qa_diagnostic_for_zero_shot_common` | QADYNAMICS: Training Dynamics-Driven Synthetic QA Diagnostic for Zero-Shot Commonsense Question Answering | Paper / dataset | QADYNAMICS benchmark frozen evaluated examples | 300 | accuracy |
| `republicqa` | RepublicQA | Paper / dataset | RepublicQA benchmark frozen evaluated examples | 300 | accuracy |
| `r_o_mqa_a_benchmark_for_robust_multi_evidence_multi_answer_question_answering` | RoMQA | Paper / dataset | RoMQA public gold development data | 300 | f1 |
| `sciknoweval` | SciKnowEval MCQA | Paper / dataset | ShAIkespear SciKnowEval_mcqa multiple-choice question answering benchmark | 300 | accuracy |
| `scitat_a_question_answering_benchmark_for_scientific_tables_and_text_covering_di` | SciTaT | Paper / dataset | SciTaT question answering benchmark for scientific tables and text | 300 | exact_match_and_f1 |
| `sealqa` | SealQA | Paper / dataset | SealQA public parquet benchmark assets from vtllms/sealqa | 254 | accuracy |
| `sec_qa_v1` | SecQA v1 | InspectAI | SecQA v1 InspectAI frozen samples | 110 | accuracy |
| `sec_qa_v1_5_shot` | SecQA v1 5-shot | InspectAI | SecQA v1 5-shot InspectAI frozen samples | 110 | accuracy |
| `sec_qa_v2` | SecQA v2 | InspectAI | Inspect Evals SecQA v2 frozen InspectAI samples | 100 | accuracy |
| `sec_qa_v2_5_shot` | SecQA v2 5-shot | InspectAI | SecQA v2 5-shot InspectAI frozen samples | 100 | accuracy |
| `sevenllm_qa_en` | SEvenLLM English QA | InspectAI | SEvenLLM English QA benchmark frozen random sample | 300 | rouge_l_and_semantic_similarity |
| `ska_bench_a_fine_grained_benchmark_for_evaluating_structured_knowledge_understan` | SKA-Bench: A Fine-Grained Benchmark for Evaluating Structured Knowledge Understanding of LLMs | Paper / dataset | SKA-Bench frozen evaluated examples | 233 | f1 |
| `squad` | SQuAD | InspectAI | SQuAD v2 validation split frozen InspectAI samples | 300 | f1 |
| `tempanswerqa_temptabqa` | TempAnswerQA and TempTabQA | Paper / dataset | TempAnswerQA and TempTabQA benchmark question sets | 300 | mean_exact_match |
| `temptabqa` | TempTabQA | Paper / dataset | TempTabQA public benchmark QA pairs and table annotations | 300 | normalized_exact_match_f1_rouge_meteor |
| `truthfulqa` | TruthfulQA | Paper / dataset | TruthfulQA multiple-choice benchmark examples | 300 | accuracy |
| `unseentimeqa` | UnSeenTimeQA | Paper / dataset | UnSeenTimeQA public benchmark data from the nurakib/UnSeenTimeQA repository | 300 | accuracy |

### Instruction Following and Writing

6 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `assistant_bench_closed_book_one_shot` | AssistantBench Closed Book One Shot | InspectAI | AssistantBench public validation split with deterministic local one-shot expansion | 50 | accuracy |
| `assistant_bench_closed_book_zero_shot` | AssistantBench Closed Book Zero Shot | InspectAI | AssistantBench closed-book zero-shot frozen local samples | 50 | accuracy |
| `ifeval` | IFEval | InspectAI | IFEval local frozen samples | 300 | prompt_level_strict_acc |
| `s_ci_dqa_a_deep_reading_comprehension_dataset_over_scientific_papers` | SciDQA: A Deep Reading Comprehension Dataset over Scientific Papers | Paper / dataset | SciDQA benchmark frozen evaluated examples | 300 | rougeL_precision |
| `unveiling_the_essence_of_poetry_introducing_a_comprehensive_dataset_and_benchmar` | Unveiling the Essence of Poetry: Introducing a Comprehensive Dataset and Benchmark for Poem Summarization | Paper / dataset | PoemSum benchmark test split | 300 | rougeL |
| `writingbench` | WritingBench | Paper / dataset | X-PLUG/WritingBench benchmark_all.jsonl | 300 | accuracy |

### Other Specialized Benchmarks

60 environments.

| Environment | Dataset / paper name | Source type | Source | Samples | Metric |
|---|---|---|---|---:|---|
| `acpbench` | ACPBench | Paper / dataset | ACPBench Hard generation test split from the ACPBench benchmark | 300 | average_exact_match |
| `agie_sat_en` | AGIEval SAT English | InspectAI | AGIEval SAT English frozen InspectAI samples | 206 | accuracy |
| `agie_sat_en_without_passage` | AGIEval SAT-EN Without Passage | InspectAI | AGIEval SAT English without passage frozen InspectAI samples | 206 | accuracy |
| `air_bench` | AIR-Bench 2024 | InspectAI | AIR-Bench 2024 frozen InspectAI samples | 300 | accuracy_by_category |
| `analobench` | AnaloBench | Paper / dataset | AnaloBench public dataset from JHU-CLSP | 300 | official_accuracy |
| `bannerd` | BanNERD | Paper / dataset | BanNERD official coNLL_format test split | 300 | entity_micro_f1 |
| `bbq` | BBQ | InspectAI | BBQ benchmark frozen InspectAI samples | 300 | accuracy |
| `criticbench` | CriticBench | Paper / dataset | CriticBench benchmark frozen test examples | 300 | task_macro_average |
| `dependeval` | DependEval | Paper / dataset | DependEval dependency recognition benchmark task2 examples | 300 | exact_match |
| `d_i_n_e_r_a_large_realistic_dataset_for_evaluating_compositional_generalization` | DiNeR TMCD Dish Name Recognition | Paper / dataset | DiNeR TMCD test split from the official DiNeR dataset | 300 | official_f1 |
| `dsdbench` | DSDBench | Paper / dataset | DSDBench public benchmark data and official exact-match evaluation assets | 300 | dsdbench_exact_match |
| `e_xplain_cpe` | ExplainCPE | Paper / dataset | ExplainCPE public official test split from the HITsz-TMG ExplainCPE repository | 190 | answer_accuracy |
| `eiffel` | EIFFEL | Paper / dataset | OpenLLM-France/EIFFEL public test split | 300 | accuracy |
| `emobench` | EmoBench | Paper / dataset | EmoBench public dataset from Hugging Face and the official EmoBench repository | 300 | task_lang_macro_average |
| `exposing_numeracy_gaps` | Exposing Numeracy Gaps | Paper / dataset | NumericBench benchmark frozen evaluated examples | 300 | accuracy |
| `fineval` | FinEval Multiple Choice | Paper / dataset | FinEval public multiple-choice test split | 170 | accuracy |
| `fortress_benign` | Fortress Benign | InspectAI | Fortress benign benchmark frozen samples | 300 | accuracy |
| `geogrambench` | GeoGramBench | Paper / dataset | GeoGramBench public benchmark data from the official repository | 300 | overall.pass_at_1 |
| `grace_a_granular_benchmark_for_evaluating_model_calibration_against_human_calibr` | GRACE: A Granular Benchmark for Evaluating Model Calibration against Human Calibration | Paper / dataset | GRACE public buzzpoints benchmark frozen evaluated examples | 239 | cal_score |
| `groundcocoa` | GroundCocoa | Paper / dataset | GroundCocoa public benchmark data from OSU-NLP-Group/GroundCocoa | 300 | accuracy |
| `h_ard2_v_erify` | Hard2Verify | Paper / dataset | Salesforce/Hard2Verify public test split | 200 | step_level.balanced_acc |
| `hellaswag` | HellaSwag | InspectAI | HellaSwag benchmark frozen InspectAI samples | 300 | accuracy |
| `h_ella_s_wag_pro_a_large_scale_bilingual_benchmark_for_evaluating_the_robustness` | HellaSwag-Pro | Paper / dataset | HellaSwag-Pro large-scale bilingual robustness benchmark frozen examples | 300 | accuracy_norm |
| `hypospace_a_diagnostic_benchmark_for_set_valued_hypothesis_generation_under_unde` | HypoSpace: A Diagnostic Benchmark for Set-Valued Hypothesis Generation under Underdetermination and Sublinear Coverage Bounds | Paper / dataset | HypoSpace Boolean benchmark bundled complete boolean configuration | 78 | recovery_rate_mean |
| `lifbench` | LIFBench | Paper / dataset | LIFBench frozen benchmark prompts | 300 | total_score |
| `lifebench` | LIFEBench | Paper / dataset | LIFEBench official frozen benchmark data | 300 | equal_to_score |
| `lingoly_too` | LingOly Too | InspectAI | Inspect Evals LingOly Too frozen samples | 300 | original_mean |
| `mafalda` | MAFALDA | Paper / dataset | MAFALDA official gold standard dataset from the public GitHub repository | 200 | micro_f1 |
| `mixeval_deriving_wisdom_of_the_crowd_from_llm_benchmark_mixtures` | MixEval: Deriving Wisdom of the Crowd from LLM Benchmark Mixtures | Paper / dataset | MixEval benchmark frozen evaluated examples | 300 | overall_accuracy |
| `multi_logieval` | Multi-LogiEval | Paper / dataset | Multi-LogiEval public benchmark data from the official repository | 300 | accuracy |
| `musr` | MuSR | InspectAI | MuSR benchmark frozen samples | 300 | accuracy |
| `novbench` | NovBench | Paper / dataset | NovBench official dataset from the academic paper novelty assessment benchmark | 300 | Relevance, Correctness_distribution_accuracy, Coverage, Clarity |
| `paws` | PAWS | InspectAI | PAWS frozen InspectAI samples | 300 | accuracy |
| `personality_TRAIT` | personality_TRAIT | Paper / dataset | TRAIT personality benchmark frozen evaluated examples | 300 | overall_high_choice_rate |
| `perspectra` | PerSpectra | Paper / dataset | PerSpectra public benchmark data from the ICLR 2026 PerSpectra repository | 300 | macro_task_accuracy |
| `phagebench` | PhageBench | Paper / dataset | PhageBench benchmark data from the public Phage-Bench project | 300 | accuracy |
| `policybench` | PolicyBench | Paper / dataset | PolicyBench public data from PolicyLLM | 300 | overall_accuracy |
| `pre_flight` | Pre-Flight | InspectAI | Inspect Evals Pre-Flight benchmark frozen samples | 300 | accuracy |
| `prime` | PRIME | Paper / dataset | wonderful9462/PRIME benchmark | 300 | overall_accuracy |
| `pub` | PUB | Paper / dataset | PUB public dataset from cfilt/PUB | 300 | accuracy |
| `questbench` | QuestBench | Paper / dataset | QuestBench public benchmark data from Google DeepMind | 300 | accuracy |
| `race_h` | RACE-H | InspectAI | RACE-H benchmark frozen InspectAI samples | 300 | accuracy |
| `r_ole_c_onflict_b_ench_a_benchmark_of_role_conflict_scenarios_for_evaluating_llm` | RoleConflictBench | Paper / dataset | RoleConflictBench benchmark frozen evaluated examples | 300 | sensitivity_score |
| `roundtripcodeeval` | RoundTripCodeEval | Paper / dataset | RoundTripCodeEval frozen compression and decompression prompt benchmark | 300 | pass_at_1 |
| `sad_facts_human_defaults` | SAD facts_human_defaults | InspectAI | Situational Awareness Dataset facts_human_defaults fixed global random sample | 300 | accuracy |
| `sad_facts_llms` | SAD facts_llms | InspectAI | SAD facts_llms frozen InspectAI samples | 249 | accuracy |
| `sad_influence` | SAD Influence | InspectAI | SAD Influence benchmark frozen full sample set | 256 | accuracy |
| `sad_stages_full` | SAD Stages Full | InspectAI | SAD stages full benchmark frozen multiple-choice records | 300 | accuracy |
| `sad_stages_oversight` | SAD stages_oversight | InspectAI | SAD stages oversight benchmark frozen random sample | 300 | accuracy |
| `scibench` | SciBench | Paper / dataset | SciBench public scientific problem benchmark | 300 | accuracy |
| `scitab` | SciTab | Paper / dataset | SciTab public dataset from the official XinyuanLu00/SciTab repository | 300 | macro_f1 |
| `sevenllm_mcq_en` | SEvenLLM English MCQ | InspectAI | SEvenLLM English multiple-choice frozen InspectAI samples | 50 | accuracy |
| `sirbench` | SIRBench-V1 DNA Translator | Paper / dataset | SIRBench-V1 official DNA translator subsets from thunlp/SIR-Bench | 200 | dna_translator_accuracy |
| `supergleber` | SuperGLEBer Hotel Aspect | Paper / dataset | SuperGLEBer Hotel_Aspect test split from the LSX-UniWue SuperGLEBer benchmark | 300 | micro_f1 |
| `t_2_r_bench_a_benchmark_for_real_world_table_to_report_task` | T2R-Bench | Paper / dataset | T2R-Bench real world table-to-report benchmark frozen evaluated examples | 261 | key_point_coverage |
| `text2distbench` | Text2DistBench | Paper / dataset | Text2DistBench public benchmark configs | 300 | mean_1_minus_tvd |
| `thunder_k_o_nub_ench` | Thunder-KoNUBench | Paper / dataset | Thunder-KoNUBench official test split from the public benchmark repository | 300 | overall_acc_norm |
| `ttt_bench` | TTT-Bench | Paper / dataset | TTT-Bench dataset from amd/TTT-Bench | 300 | accuracy |
| `winogrande` | WinoGrande | InspectAI | WinoGrande benchmark frozen InspectAI samples | 300 | accuracy |
| `wxi_mpact_b_ench_a_disruptive_weather_impact_understanding_benchmark_for_evaluat` | WXImpactBench: A Disruptive Weather Impact Understanding Benchmark | Paper / dataset | WXImpactBench disruptive weather impact understanding benchmark | 300 | macro_f1 |
