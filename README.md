# RSI-Dojo

RSI-Dojo is an open-source collection of executable environments for studying
LLM agents that automate LLM post-training. Each environment is designed to let
an agent analyze a target benchmark, prepare or construct training data, launch
post-training runs, evaluate checkpoints, diagnose failures, and iterate toward
an improved model.

The project is intended to support research on autonomous model-improvement
agents and recursive self-improvement workflows. Instead of only evaluating
whether an agent can solve a static task, RSI-Dojo focuses on whether an agent
can run the model-development loop itself: data selection, training, validation,
and revision.

This repository will provide:

- The executable post-training environments used by RSI-Dojo.
- The normalized benchmark interfaces and evaluation entry points.
- The list of datasets and papers used to construct the environments.
- Utilities for running, validating, and reproducing the environments.

The environment and dataset materials are being organized for release. More
files and documentation will be added as the release is finalized.

