# RSI-Dojo

Training LLM Agents to Automate LLM Post-Training.

RSI-Dojo is an open-source collection of executable environments for studying
LLM agents that automate LLM post-training. Each environment is designed to let
an agent analyze a target benchmark, prepare or construct training data, launch
post-training runs, evaluate checkpoints, diagnose failures, and iterate toward
an improved model.

## Overview

The project is intended to support research on autonomous model-improvement
agents and recursive self-improvement workflows. Instead of only evaluating
whether an agent can solve a static task, RSI-Dojo focuses on whether an agent
can run the model-development loop itself: data selection, training, validation,
and revision.

RSI-Dojo turns post-training into executable long-horizon environments. In each
environment, an agent is given a base model, a target evaluation, and a local
workspace. The agent must inspect failures, identify useful training data,
configure post-training, run evaluations, and decide how to continue. This makes
the environment suitable for collecting and evaluating full model-improvement
trajectories rather than isolated final answers.

![RSI-Craft pipeline overview](assets/method.png)

RSI-Craft builds the environment collection in three stages. It first searches
recent top-venue papers and InspectAI tasks for candidate benchmarks, then
instantiates executable environments by recovering data, metrics, dependencies,
and evaluation code. Finally, it filters the environments for reliability and
discriminability so that retained tasks provide useful feedback for iterative
post-training.

The full RSI-Dojo release is organized around:

- Executable post-training environments.
- Normalized benchmark interfaces and evaluation entry points.
- Dataset and paper provenance for the environments.
- Utilities for running, validating, and reproducing the environments.

The released environment list is available in
[ENVIRONMENTS.md](ENVIRONMENTS.md). It groups the 281 normalized environments
by domain, records each environment's originating paper, public dataset, or
InspectAI task source, and summarizes the runtime dependencies used by
`run1.sh`. Some environments use an LLM judge and require
`EVAL_OPENAI_AK` and `EVAL_OPENAI_ENDPOINT` to be configured before running.

## Results Snapshot

![PostTrainBench performance comparison](assets/performance.png)

![RSI-Dojo result summary](assets/results.png)

Fine-tuning on RSI-Dojo trajectories improves both evaluated model families on
PostTrainBench and PostTrainBench-Lite. RSI-Dojo-35B-A3B reaches 29.95 on
PostTrainBench and 53.29 on PostTrainBench-Lite under the reported evaluation
setting. It also completed all 28 PostTrainBench settings and improved the
trained model in 26 of them. Across 175 total iterations, 61 iterations produced
effective improvements.

## Release Progress

- [x] Environments
- [ ] Data
- [ ] Models and code

The materials are being organized for staged release. Items will be checked off
as they become available.
