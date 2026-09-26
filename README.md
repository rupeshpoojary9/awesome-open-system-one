# Awesome Open System One [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of the **open** System One ecosystem: open models, training methods, independent benchmarks, and the calibration and constrained-decoding tooling that make typed, confidence-aware decisions work.

"System One models" (a term from TypeSafe's Jev launch, after Kahneman's System 1) make fast, typed, calibrated decisions that software consumes directly, classify, route, score, gate, instead of generating text you parse and hope about. Jev itself is closed, hosted, and waitlisted. This list tracks the **open** side: reproductions you can run, independent evaluations you can check, and the underlying techniques (calibrated confidence, constrained decoding, conformal abstention) that predate the name and outlive any one product.

Every link is verified. Entries are open source or openly readable. For lists of projects *using* the closed Jev, see the other awesome-jev lists; this one is deliberately about what you can run and audit yourself.

## Contents

- [What Is a System One Model](#what-is-a-system-one-model)
- [Open Models and Reproductions](#open-models-and-reproductions)
- [Independent Benchmarks and Evaluations](#independent-benchmarks-and-evaluations)
- [Calibration and Selective Prediction](#calibration-and-selective-prediction)
- [Constrained and Structured Decoding](#constrained-and-structured-decoding)
- [Reference and Reading](#reference-and-reading)

## What Is a System One Model

A System One model takes a block of state plus a set of typed questions and returns, in one parallel pass, a typed answer per question with a calibrated confidence, rather than a token-by-token text string. The output is schema-valid by construction (it must be one of the options you declared), and the confidence is meant to be trustworthy enough to branch on. The category is new as a name; the ingredients, zero-shot classification, calibrated probabilities, constrained decoding, conformal abstention, are established and open, which is what this list collects.

## Open Models and Reproductions

Open models and runnable replicas of the System One idea.

- [poorjev](https://github.com/rupeshpoojary9/poorjev) - Local-first System One layer on commodity models with provably calibrated confidence (measured ECE 0.170 to 0.071), typed primitives, no API key.
- [von](https://github.com/wfzyx/von) - Open-source System One decision model: sub-15ms, non-autoregressive, local drop-in alternative to Jev.
- [Laya](https://laya.convaiinnovations.com/) - A 421M non-autoregressive System One decision engine with RLCD-trained calibrated probabilities and multilingual support.
- [NanoJev](https://github.com/chenyangcun/NanoJev) - A minimal nanoGPT-style replica of Jev: parallel decisions, dynamic candidates, and an end-to-end training pipeline.
- [nanojev (single-file)](https://github.com/novvoo/nanojev) - A single-file, MIT-licensed educational implementation with a small serving UI and HTTP API.
- [kev](https://github.com/jaredpalmer/kev) - A tiny, trainable family of Jev-like decision models built on Qwen3.5 that you can fine-tune and run locally.
- [SemIf](https://github.com/TheoLeeCJ/SemIf) - Independent "semantic if" engine: typed decisions from open models on a single home GPU, unaffiliated with Jev or TypeSafe.
- [laya-mlx](https://github.com/mizorewww/laya-mlx) - Native Apple Silicon (MLX) runtime for running the open Laya typed-decision model locally, non-autoregressive with no text generation.
- [simple-jev](https://github.com/featherless-ai/simple-jev) - Turns any open model into a typed classifier or Jev-style decision endpoint.
- [OpenThai-SystemOne](https://github.com/iapp-technology/openthai-systemone) - Open (Apache-2.0) Thai and English System One decision model, 0.8B with a 256-way slot head.
- [sokudan](https://github.com/hiroki-abe-58/sokudan) - Apache-2.0 Japanese System One model (314.6M, ModernBERT-ja); 3-seed mean bool AUROC 0.789 on its own CC BY 4.0 bench_ja; bool under-predicts true.

## Independent Benchmarks and Evaluations

Third-party evaluations of typed decision models, measuring what the marketing pages assert.

- [jev-benchmarks](https://github.com/AbdelStark/jev-benchmarks) - Probability-aware evaluation for typed decision models: calibration, selective risk, latency, and reproducible benchmarks.
- [jev-baselines-eval](https://github.com/ickma2311/jev-baselines-eval) - Pre-registered independent eval of Jev against a nano-class LLM, a frontier LLM, and a supervised encoder on Banking77 and CLINC150.
- [jev-eval](https://github.com/4esv/jev-eval) - Independent eval of Jev vs a frontier LLM across labelled classification tasks: accuracy, calibration, latency, and cost.
- [JevBench](https://github.com/fstandhartinger/jevbench) - Open benchmark for Jev-class typed decision models, scoring accuracy, cost, latency, and reliability.

## Calibration and Selective Prediction

The techniques that make a confidence score trustworthy, and let a model abstain instead of guessing.

- [conformal-prediction](https://github.com/aangelopoulos/conformal-prediction) - Angelopoulos and Bates: lecture notes and runnable notebooks on conformal prediction and distribution-free uncertainty, the basis for principled abstention.
- [MAPIE](https://github.com/scikit-learn-contrib/MAPIE) - Scikit-learn-compatible library for prediction intervals and sets with guaranteed coverage, usable for the "escalate when unsure" path.
- [jevcal](https://github.com/abhixhek/jevcal) - Calibrates, thresholds, and drift-checks the confidence scores of typed decision models so you stop guessing cutoffs.

## Constrained and Structured Decoding

Making output schema-valid by construction rather than by parsing, an adjacent lineage that System One models formalize.

- [Outlines](https://github.com/dottxt-ai/outlines) - Structured generation that constrains a model to a grammar, regex, or JSON schema, so invalid output is impossible.
- [XGrammar](https://github.com/mlc-ai/xgrammar) - Fast, flexible structured-generation engine for constraining LLM outputs to a grammar with low overhead.
- [Instructor](https://github.com/567-labs/instructor) - Structured outputs from LLMs via typed schemas, with validation and retries; a common baseline for typed decisions today.
- [Guidance](https://github.com/guidance-ai/guidance) - Constrained generation with interleaved control, so structure is enforced during decoding rather than after.
- [LM Format Enforcer](https://github.com/noamgat/lm-format-enforcer) - Enforces JSON schema or regex on LLM output during generation.

## Reference and Reading

- [Introducing System One Models and Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev) - TypeSafe's launch post that named the category and stated the thesis.
- [System One (TypeSafe docs)](https://docs.typesafe.ai/concepts/system-one) - The concept and interface as defined by the model's authors.
- [Building a Harness with Jev](https://www.langchain.com/blog/building-a-harness-with-jev) - LangChain's practical walkthrough of wiring a decision model into an agent harness.
- [On Calibration of Modern Neural Networks](https://arxiv.org/abs/1706.04599) - Guo et al., 2017. Introduces temperature scaling and ECE, the calibration foundations these models rely on.

## Contributing

Contributions welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md). In short: the entry must be open source or openly readable, on-topic (open System One models, their evaluation, or the calibration and constrained-decoding techniques behind them), described in one factual line, and the link must work.
