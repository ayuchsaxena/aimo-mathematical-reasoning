# AI Mathematical Olympiad — Model Experiments

This repository documents experiments with AI models attempting competition-style mathematical reasoning problems for the AI Mathematical Olympiad (AIMO).

The central question was: **how do model choice, prompts, and inference settings affect a model's attempts to solve a maths problem and return an answer?**

## My contribution

My role focused on **model testing and evaluation**. I helped test model configurations and prompt approaches, review inference behaviour, and inspect the generated responses. The experiments included Qwen- and DeepSeek-based models, different model sizes, quantized configurations, and inference setups.

The goal was to understand how these setups behaved in practice and to document the outputs for further evaluation. Model development and fine-tuning were contributed by collaborators; this repository does not attribute that work to me.

## Experiment overview

| Item | What is documented |
| --- | --- |
| Selected notebooks | 5 |
| Model sizes explored | 7B and 14B |
| Model families/configurations | DeepSeek-R1 distilled models based on Qwen, Qwen prompt experiments, and AutoRound variants |
| Inference engine | vLLM |
| Recorded vLLM versions | 0.7.1 and 0.7.3 |
| Example inference setup | 4 visible GPUs, tensor parallelism of 4, and a maximum sequence length of 12,288 tokens in logged configurations |

These details describe the saved notebooks and logs. They do **not** establish that one configuration performed better than another.

## Mistakes we identified

Reviewing the notebooks helped us identify a few mistakes and areas to improve:

1. **Too few questions:** We tested 96 responses, but they covered only three different problems. This was not enough to judge how well the models solve maths problems in general.
2. **Scoring issues:** Some notebooks used predefined answers for selected questions. This helped with testing, but we needed a more reliable way to check answers.
3. **Answer-reading errors:** Our code could fail to read some answers correctly, especially when the answer format was unusual.
4. **Skipped questions:** Some local tests skipped questions that were outside a small selected group, so the results did not represent a full evaluation.
5. **Unclear prompt comparisons:** We tried different prompts, but we did not compare them consistently enough to know which worked best.
6. **Inconsistent test settings:** We changed model settings and configurations across experiments, making the results harder to compare fairly.
7. **No proven improvement:** We had a baseline notebook, but we did not have enough consistent results to show that one setup performed better than another.

These lessons showed us that successful model runs do not automatically mean correct answers or better performance. We needed more questions, more consistent testing, and a clearer way to check and compare results.

## Evaluation data

The saved evaluation files contain:
- `reference.csv`: 10 reference problems.
- Three response files, each with 32 generated responses for a single problem (96 responses across 3 distinct problems).

The response files correspond to:
- `solution-variant-1.csv` — delightful-sequence problem.
- `solution-variant-2.csv` — triangle geometry problem.
- `solution-variant-3.csv` — tennis-tournament pairing problem.

The 96 responses are repeated attempts on only three distinct questions; they should not be interpreted as 96 independently evaluated problems. The available files do not include a complete, verified answer key and consistent scoring results sufficient to substantiate an accuracy figure. **For that reason, this README does not report a measured accuracy percentage or a verified accuracy improvement.**

## What a stronger evaluation should do

1. Use a fixed, representative set of questions with independently verified reference answers.
2. Record a clearly defined baseline model and its full inference settings.
3. Change one variable at a time, keeping the evaluation set and scoring rules consistent.
4. Unit-test answer extraction for missing, malformed, multiple, and nested boxed answers.
5. Separate model outputs from parsing failures, skipped questions, timeouts, and fallback values.
6. Report exact-answer accuracy only when the scoring method and results can be reproduced.
7. Track parse success, invalid/unparseable answers, inference time, memory/resource use, and per-question results.
8. Run repeated trials when sampling introduces variability, and report the variation rather than only the best run.

The checklist in [evaluation/README.md](evaluation/README.md) outlines additional evaluation considerations. Until those steps are completed and results are recorded, this repository should be treated as an experiment log—not a validated benchmark or an official AIMO competition result.

## Selected notebooks

| Notebook | What it covers |
| --- | --- |
| [AIMO2 inference pipeline](01-aimo2-inference-pipeline.ipynb) | Running the inference pipeline and handling candidate answers |
| [Qwen 14B prompt experiments](02-qwen-14b-prompt-experiments.ipynb) | Testing prompts with a 14B model configuration |
| [AutoRound inference v2](03-autoround-inference-v2.ipynb) | Testing an AutoRound model configuration |
| [AutoRound baseline](04-autoround-inference-baseline.ipynb) | An inference configuration intended to serve as a baseline |
| [Qwen 7B prompt evaluation](05-qwen-7b-prompt-evaluation.ipynb) | Experiments with a 7B model configuration |

## What these experiments suggest

Model size alone does not tell the whole story. Prompt wording, inference settings, answer extraction, scoring, and runtime constraints all affect the outputs and the ability to evaluate them. Determining whether a change helps requires running configurations on the same questions under the same scoring rules.

These notebooks capture exploratory testing and evaluation work. They do not establish a verified ranking of configurations or an official AIMO result.

## Running the notebooks

The notebooks were created for Kaggle-style GPU environments and may require GPU access, specific libraries, and model files that are not included here. Review each notebook's setup and model paths before running it. Some notebooks log CUDA-based inference with vLLM and tensor parallelism across four GPUs; a standard laptop may not meet those requirements.

Some work originated from external notebooks and model projects. Check original sources and licences before redistributing or reusing third-party code or model files.

## Acknowledgements

Thanks to the collaborators whose model work and experiments informed this project. My contribution focused on testing model configurations, reviewing inference behaviour, and evaluating the available outputs. Model development and fine-tuning should be credited to their respective contributors.
