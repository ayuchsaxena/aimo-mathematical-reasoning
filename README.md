# AIMO Mathematical Reasoning

Experiments in mathematical-reasoning model inference, prompt construction, model configuration, and evaluation for the AI Mathematical Olympiad (AIMO).

## Project overview

This repository collects selected notebook experiments from AIMO-related work. The notebooks explore inference pipelines, prompt strategies, and different Qwen/DeepSeek model configurations. They should be treated as experimental artifacts, not as evidence of comparative accuracy unless measured results are explicitly reported.

## Notebooks

| Notebook | Focus |
| --- | --- |
| [01 — AIMO2 inference pipeline](notebooks/01-aimo2-inference-pipeline.ipynb) | Inference pipeline and candidate-answer handling |
| [02 — Qwen 14B prompt experiments](notebooks/02-qwen-14b-prompt-experiments.ipynb) | Prompt construction and reasoning experiments |
| [03 — AutoRound inference v2](notebooks/03-autoround-inference-v2.ipynb) | AutoRound model artifact and inference configuration |
| [04 — AutoRound baseline](notebooks/04-autoround-inference-baseline.ipynb) | Separate model artifact and inference configuration |
| [05 — Qwen 7B prompt evaluation](notebooks/05-qwen-7b-prompt-evaluation.ipynb) | Experiments with a 7B model configuration |

## Contribution and attribution

My contribution to this work focused on testing and evaluating Qwen and other mathematical-reasoning models, including examining inference behaviour and experimental configurations. Model development, fine-tuning, and other experimentation were contributed by collaborators; contributions should be attributed to the relevant original authors rather than implying that all model work was mine.

Some notebooks originated from Kaggle work. Original sources and licensing/redistribution details should be retained and verified before redistribution. This repository does not claim ownership of the underlying model weights or third-party artifacts.

## Evaluation status and limitations

Saved model-loading and generation logs show that code paths were exercised, but do not by themselves establish exact-answer accuracy or a reliable comparison between configurations. Any claims about performance should be supported by a reproducible evaluation set and explicit metrics.

Before treating results as benchmark evidence, inspect the notebooks for competition-specific shortcuts, validate answer extraction/selection behaviour, and confirm that local runs execute actual inference rather than returning preset outputs.

See [evaluation/README.md](evaluation/README.md) for the proposed evaluation approach.

## Runtime

These notebooks were originally designed for Kaggle-style GPU environments and may depend on large model artifacts and libraries such as vLLM. They are not guaranteed to run unchanged on a standard laptop. Review each notebook's imports, model paths, hardware requirements, and runtime configuration before execution.

## Scope

This is an experimental portfolio project documenting model testing and inference experiments. It is not an official AIMO resource and does not claim an independently verified competition result.
