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

## Mistakes and limitations identified in review

Reviewing the notebooks surfaced several concrete weaknesses in the experimental design and evaluation code. These are useful lessons from the work, not claims that the models themselves necessarily failed for each reason.

1. **The evaluation set was too small and uneven.** The saved response files contain 96 generations across only three distinct questions, with 32 attempts per question. Repeated generations can help study variability, but they do not substitute for a broad, representative problem set. Three problems are far too few to support general claims about mathematical reasoning.

2. **The scoring path was not a clean, independent evaluation.** Some notebooks include hard-coded question-to-answer mappings for a small set of known problems and use them to print a running score. That is useful as a local debugging aid, but it is not a substitute for a separate, verified evaluation pipeline. The fallback answer of `0` for an unrecognised question can also make an unknown question look like it has a valid reference answer. The scoring should fail explicitly when no verified answer exists.

3. **Some local runs intentionally skipped most questions.** For example, the Qwen 14B experiment's `_should_skip` method returns a fallback answer for questions outside a small selected subset when not running in the competition environment. That can be sensible for targeted debugging, but results from such a run must not be treated as full-dataset evaluation. Skipped questions and fallback outputs need to be recorded separately from model predictions.

4. **Answer extraction is fragile.** The notebooks use a regular expression based on `oxed{(.*?)}` to extract boxed answers. It can find the text inside a typical `\\boxed{...}` expression, but it does not correctly handle nested braces and may truncate expressions that contain braces. Empty or malformed outputs are filtered, while answer selection can fall back to `210`; those cases should be counted as extraction failures, not silently treated as ordinary predictions.

5. **The voting and fallback rules can hide failure modes.** Majority voting over generated answers can be useful, but the current approach only votes over outputs that can be parsed as integers. It does not, by itself, establish that the majority answer is correct. A fixed fallback such as `210` when no usable answer is found can obscure the difference between a genuine model prediction and a failed generation/parse. Report parse success rate and fallback rate alongside accuracy.

6. **Prompt comparisons are confounded.** The notebooks vary prompt wording and assistant thought prefixes, but the saved results do not provide a complete, consistently scored, per-question comparison under a controlled protocol. Some variants also repeat prompt structures. Without holding the model, question set, decoding settings, and scoring procedure constant while changing one factor at a time, we cannot attribute differences to prompt wording.

7. **Reproducibility is incomplete.** The notebooks use different random seeds, model paths, batch sizes, context limits, quantization settings, and inference settings. The presence of seed-setting code does not guarantee deterministic outputs; for example, CUDA/cuDNN settings and sampling can still affect reproducibility. A fair comparison needs a recorded configuration for every run, repeated trials where appropriate, and a clear explanation of which settings changed.

8. **The saved baseline is not enough to establish an improvement.** A notebook named “baseline” is not automatically a valid baseline comparison. To claim an improvement, the baseline and candidate configuration must be run on the same verified questions with the same scoring and comparable resource/runtime constraints, and the results must be reported side by side.

9. **Competition-oriented runtime logic complicates offline interpretation.** The notebooks contain time cutoffs, environment-dependent model paths, and competition/local-run branches. These may be necessary for the target runtime, but they make it important to distinguish a successful pipeline execution from a completed, comparable evaluation. Timeouts, skipped items, and environment-specific behaviour should be logged explicitly.

These issues mean the saved work is best interpreted as **exploratory model testing**, not a validated benchmark. The key improvement is to separate inference, answer extraction, reference-answer validation, scoring, and reporting into testable components.

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
