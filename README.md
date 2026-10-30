# AI Mathematical Olympiad — Model Experiments

This repository contains selected experiments with AI models solving competition-style mathematics problems for the AI Mathematical Olympiad (AIMO).

The question we explored was simple: **how do model choice, prompts, and inference settings affect a model's attempt to solve a maths problem and return an answer?**

## What we worked on

My contribution focused on testing model setups and reviewing inference behaviour, especially with Qwen- and DeepSeek-based models. The notebooks explore different prompt approaches, model sizes, quantized model configurations, and ways to run inference.

In practical terms, we tried different ways to run a model and guide its response, then kept notebooks documenting those experiments. Model development and fine-tuning were also contributed by collaborators; this repository does not claim that all model work was mine.

## A few concrete details

| Item | What the notebooks show |
| --- | --- |
| Selected notebooks | 5 |
| Model sizes explored | 7B and 14B |
| Model families/configurations | DeepSeek-R1 distilled models based on Qwen, Qwen prompt experiments, and AutoRound variants |
| Inference engine | vLLM |
| Recorded vLLM versions | 0.7.1 and 0.7.3 |
| Example inference setup | 4 visible GPUs, tensor parallelism of 4, and a maximum sequence length of 12,288 tokens in the logged configurations |
| Measured accuracy | Not yet established through a controlled, documented evaluation in this repository |

These are details from the saved notebooks and their logs, not a claim that one model or configuration performed best.

## Saved problem and response data

The attached evaluation files contain:
- `reference.csv`: 10 reference problems.
- Three response files, each containing 32 generated responses for one problem (96 responses total across 3 problems).

The three response files are being organized as:
- `solution-variant-1.csv` — responses for the delightful-sequence problem.
- `solution-variant-2.csv` — responses for the triangle geometry problem.
- `solution-variant-3.csv` — responses for the tennis-tournament pairing problem.

These are repeated model responses to three problems, not 96 distinct questions. The available files do not provide a verified answer key for all 10 reference problems, so they should be treated as raw experiment outputs rather than a completed accuracy benchmark.

## The early evaluation mistake: no proper baseline

One thing we would do differently is establish a baseline before comparing prompts and model configurations.

Early experiments looked at whether a setup ran and how the model generated answers, but **running successfully is not the same as solving the problems correctly**. Without a fixed set of questions, a consistent scoring method, and a baseline model to compare against, it is difficult to tell whether a prompt or configuration actually improved performance.

That makes conclusions weaker: changes in output may look promising without proving a real gain in accuracy. We should have recorded baseline exact-answer accuracy first, then changed one factor at a time and evaluated every version on the same questions.

A stronger evaluation should report:
- the number of questions tested and the exact-answer accuracy;
- the baseline model and settings;
- answer-extraction failures and invalid answers;
- inference time and resource use;
- results for each configuration under the same scoring rules.

The evaluation checklist in [evaluation/README.md](evaluation/README.md) outlines these checks. The measured results have not yet been added, so we do not claim a verified accuracy improvement.

## Selected notebooks

| Notebook | What it covers |
| --- | --- |
| [AIMO2 inference pipeline](01-aimo2-inference-pipeline.ipynb) | Running the inference pipeline and handling candidate answers |
| [Qwen 14B prompt experiments](02-qwen-14b-prompt-experiments.ipynb) | Testing prompts with a 14B model configuration |
| [AutoRound inference v2](03-autoround-inference-v2.ipynb) | Testing an AutoRound model configuration |
| [AutoRound baseline](04-autoround-inference-baseline.ipynb) | A baseline model configuration for comparison |
| [Qwen 7B prompt evaluation](05-qwen-7b-prompt-evaluation.ipynb) | Experiments with a 7B model configuration |

## What we learned

Model size alone does not tell the whole story. Prompt wording, inference settings, answer extraction, and runtime limits all matter. To know whether a change helps, the models need to be compared on the same questions with the same scoring rules.

These notebooks document experiments, not a verified ranking of the configurations or an official AIMO competition result.

## Running the notebooks

The notebooks were created for Kaggle-style GPU environments and may require GPU access, specific libraries, and model files that are not included here. Check each notebook's setup and model paths before running it. Some notebooks log CUDA-based inference with vLLM and tensor parallelism across four GPUs; a standard laptop may not meet those requirements.

Some work originated from external notebooks and model projects. Please check original sources and licences before redistributing or reusing third-party code or model files.

## Acknowledgement

Thanks to the collaborators whose model work and experiments informed this project. My documented focus was on testing model configurations and inference behaviour; model development and fine-tuning should be credited to their respective contributors.
