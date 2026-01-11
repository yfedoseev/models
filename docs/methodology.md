# Methodology

This document describes how model rankings are calculated.

## Core Principles

### 1. Primary Benchmark Ranking

Each category uses a **primary benchmark** that determines rank. Models WITH the primary benchmark always rank above models WITHOUT it.

```
Coding:     SWE-bench Verified (primary) → Aider, Terminal-Bench (tiebreakers)
Reasoning:  GPQA Diamond (primary) → FrontierMath, AIME (tiebreakers)
Knowledge:  SimpleQA Verified (primary) → HLE, MMLU-PRO (tiebreakers)
```

**Why?** Easy benchmarks (HumanEval: 90%+ common) shouldn't outrank hard benchmarks (SWE-bench: 80% is exceptional). A model with SWE-bench 75% is more capable than one with only HumanEval 97%.

### 2. Benchmark Difficulty Hierarchy

| Tier | Weight | Examples | Typical Scores |
|------|--------|----------|----------------|
| **Tier 1** (Hard) | Primary | SWE-bench, GPQA, SimpleQA | 50-85% |
| **Tier 2** (Medium) | Tiebreaker | AIME, MATH Level 5 | 60-90% |
| **Tier 3** (Easy) | Supplementary | HumanEval, MMLU, GSM8K | 85-98% |

### 3. Normalized Scoring

All benchmarks are normalized to a 0-1 scale:

| Benchmark Type | Normalization |
|----------------|---------------|
| Percentage (0-100) | Divide by 100 |
| Arena ELO (1000-1600) | `(value - 1000) / 600` |
| Already 0-1 | No change |

### 4. No Provider Bias

Rankings are calculated purely on benchmark performance. Provider identity has no effect on scoring.

---

## Categories

### Arena ELO (Human Preference)

Based on millions of blind A/B comparisons from the [LMSys Chatbot Arena](https://lmarena.ai/).

- **Source**: LMSys Arena leaderboard
- **What it measures**: Human preference in real conversations
- **Why it matters**: Captures qualities that benchmarks miss (helpfulness, tone, coherence)

### Overall

Weighted average across all available benchmarks (minimum 3 required). Tier 1 benchmarks weighted 3x, Tier 2 weighted 2x, Tier 3 weighted 1x.

### Coding / Software Engineering

**Primary Benchmark**: SWE-bench Verified (real GitHub issue resolution)

| Benchmark | Tier | Description |
|-----------|------|-------------|
| SWE-bench Verified | 1 | Real GitHub issue resolution |
| Aider Polyglot | 1 | Multi-language coding assistant |
| Terminal-Bench | 1 | CLI and terminal tasks |
| OSWorld | 1 | OS-level automation |
| LiveBench Agentic Coding | 1 | Agentic coding tasks |
| SWE-bench | 2 | Full SWE-bench (unverified) |
| LiveBench Coding | 2 | General coding tasks |
| HumanEval | 3 | Function completion (saturated) |

### Reasoning / Math

**Primary Benchmark**: GPQA Diamond (PhD-level science)

| Benchmark | Tier | Description |
|-----------|------|-------------|
| GPQA Diamond | 1 | PhD-level science questions |
| FrontierMath | 1 | Research-level mathematics |
| Humanity's Last Exam | 1 | Expert-level questions |
| SimpleBench | 1 | Hard reasoning tasks |
| MATH Level 5 | 2 | Competition mathematics |
| AIME 2024/2025 | 2 | American Invitational Math Exam |
| MMLU | 3 | Multi-task knowledge (saturated) |
| GSM8K | 3 | Grade school math (saturated) |

### Knowledge / Research

**Primary Benchmark**: SimpleQA Verified (factual accuracy)

| Benchmark | Tier | Description |
|-----------|------|-------------|
| SimpleQA Verified | 1 | Factual accuracy |
| Humanity's Last Exam | 1 | Expert-level knowledge |
| Deep Research Bench | 1 | Research capability |
| MMLU-PRO | 2 | Harder MMLU variant |
| IFEval | 2 | Instruction following |
| MMLU | 3 | Broad academic knowledge (saturated) |
| TriviaQA | 3 | Factual recall (easy) |

### Hard / Frontier

The most challenging benchmarks. All are Tier 1 (no easy benchmarks).

| Benchmark | Description |
|-----------|-------------|
| ARC-AGI-2 | Abstract reasoning |
| FrontierMath | Research-level mathematics |
| Humanity's Last Exam | Expert-level questions |
| Scale Multi-Challenge | Multi-domain challenges |
| OSWorld | OS-level automation |

---

## ROI (Return on Investment) Rankings

ROI measures performance per dollar spent:

```
ROI = Primary Benchmark Score / Average Price per 1M tokens
```

Where:
```
Average Price = (Input Price + Output Price) / 2
```

Higher ROI indicates better value. A model with ROI of 5.0 delivers 5x more performance per dollar than a model with ROI of 1.0.

### Example

| Model | SWE-bench | Avg Price | ROI |
|-------|-----------|-----------|-----|
| gpt-5-nano | 76.3% | $0.11/1M | 6.78 |
| Claude Opus 4.5 | 80.9% | $22.50/1M | 0.04 |

gpt-5-nano provides 170x better ROI for coding tasks, despite slightly lower absolute performance.

---

## Data Sources

| Data Type | Source |
|-----------|--------|
| Benchmarks | [Epoch AI](https://epoch.ai), official provider announcements |
| Arena ELO | [LMSys Chatbot Arena](https://lmarena.ai/) |
| Pricing | Official provider API pricing pages |
| Model specs | Provider documentation and APIs |

---

## Filtering

The following are excluded from rankings:

- **Non-chat models**: Embeddings, image generation, speech-to-text
- **Gateway/aggregator providers**: OpenRouter, Portkey (pass-through pricing)
- **Deprecated models**: Claude Instant, GPT-3.5, legacy snapshots
- **Meta/routing models**: Auto-routers, model mixtures

---

## Update Frequency

Rankings are regenerated weekly from fresh data sources. Benchmark scores are updated as new evaluations become available.
