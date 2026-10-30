# AI Mathematical Olympiad — Model Experiments

This repository contains selected experiments with AI models solving competition-style mathematics problems for the AI Mathematical Olympiad (AIMO).

The goal was to explore how model choice, prompts, and inference settings affect the way a model works through a math problem and produces an answer.

## What we worked on

My contribution focused on testing and evaluating model setups, especially Qwen and DeepSeek-based models. I compared prompt approaches, reviewed inference behaviour, and explored different model configurations, including AutoRound variants.

In simple terms, we tested different ways to run the models and guide their reasoning, then kept notebooks that show the approaches we explored. This repository documents those experiments; it does not claim a verified accuracy improvement or an official competition placement.

## Selected notebooks

| Notebook | What it covers |
| --- | --- |
| [AIMO2 inference pipeline](01-aimo2-inference-pipeline.ipynb) | Running the inference pipeline and handling candidate answers |
| [Qwen 14B prompt experiments](02-qwen-14b-prompt-experiments.ipynb) | Testing different prompts with a 14B model |
| [AutoRound inference v2](03-autoround-inference-v2.ipynb) | Testing an AutoRound model configuration |
| [AutoRound baseline](04-autoround-inference-baseline.ipynb) | A baseline for comparison with another configuration |
| [Qwen 7B prompt evaluation](05-qwen-7b-prompt-evaluation.ipynb) | Experiments with a smaller model and its prompt setup |

## What we learned

Model size alone does not tell the whole story. Prompt wording, inference settings, answer extraction, and runtime constraints all matter when testing math-solving systems. A useful comparison also needs the same evaluation questions and clear scoring, rather than relying only on logs or a few examples.

The notebooks are records of our experiments, not a claim that every configuration was better than the others.

## Running the notebooks

These notebooks were created for Kaggle-style environments and may require GPU access, specific libraries, and model files that are not included here. Check each notebook's setup and model paths before running it. Results should be re-evaluated on a consistent test set before drawing performance conclusions.

Some work originated from external notebooks and model projects. Please check the original sources and their licences before redistributing or reusing third-party code or model files.

## Acknowledgement

Thanks to the collaborators whose model work and experiments informed this project. The work documented here includes my focus on testing and evaluation; model development and fine-tuning should be credited to their respective contributors.
