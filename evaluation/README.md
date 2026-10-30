# Evaluation notes

The saved notebook outputs are useful records of inference experiments, but they are not a substitute for a controlled accuracy evaluation.

## Recommended checks

1. **Answer extraction:** test boxed answers, missing answers, malformed delimiters, multiple boxed answers, and nested braces.
2. **Answer selection:** test candidate lists with valid answers, invalid values, ties, and no valid candidate.
3. **Execution-path audit:** identify any competition-only branches or hard-coded return values that can bypass model inference in local runs.
4. **Exact-answer accuracy:** run on a documented set of questions with known answers and report the denominator, scoring rule, and exclusions.
5. **Operational metrics:** record extraction success, invalid-output rate, latency, and candidate agreement where feasible.
6. **Configuration comparison:** use the same questions and scoring logic for each model/configuration before making comparisons.

## Current status

This file describes recommended work; automated tests and measured metrics have not yet been added. Do not report numerical accuracy or claim one configuration is better until the evaluation has actually been run and results are recorded.

Review each notebook's original source, attribution, license, model artifact terms, and any preset-answer shortcuts before redistribution or benchmarking.
