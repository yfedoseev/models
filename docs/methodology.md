# Methodology

This document describes how model rankings are calculated.

## Core Principles

### 1. Equal Benchmark Weighting

Every benchmark within a category receives **equal weight**. This prevents cherry-picking benchmarks that favor specific models or providers.

```
Category Score = Average(benchmark_1, benchmark_2, ..., benchmark_n)
```

For example, the Coding category includes SWE-bench, HumanEval, Aider Polyglot, and Terminal-Bench. Each contributes equally to the final coding score.

### 2. Normalized Scoring

All benchmarks are normalized to a 0-1 scale for fair comparison:

| Benchmark Type | Normalization |
|----------------|---------------|
| Percentage (0-100) | Divide by 100 |
| Arena ELO (1000-1600) | `(value - 1000) / 600` |
| Already 0-1 | No change |

### 3. Minimum Benchmark Requirement

Models must have scores for at least 3 benchmarks to appear in category rankings. This prevents models with a single exceptional score from dominating rankings.

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

Simple average across all available benchmarks. Provides a holistic view of model capability.

### Coding / Software Engineering

| Benchmark | Description |
|-----------|-------------|
| SWE-bench Verified | Real GitHub issue resolution |
| HumanEval | Function completion |
| Aider Polyglot | Multi-language coding assistant |
| Terminal-Bench | CLI and terminal tasks |
| LiveBench Coding | Contamination-free coding tasks |

### Reasoning / Math

| Benchmark | Description |
|-----------|-------------|
| GPQA Diamond | PhD-level science questions |
| MATH Level 5 | Competition mathematics |
| MMLU | Multi-task knowledge |
| GSM8K | Grade school math |
| AIME 2024/2025 | American Invitational Mathematics Exam |

### Knowledge / Research

| Benchmark | Description |
|-----------|-------------|
| MMLU | Broad academic knowledge |
| SimpleQA | Factual accuracy |
| TriviaQA | Factual recall |

### Hard / Frontier

The most challenging benchmarks for current AI systems:

| Benchmark | Description |
|-----------|-------------|
| ARC-AGI-2 | Abstract reasoning |
| FrontierMath | Research-level mathematics |
| Humanity's Last Exam | Expert-level questions |

---

## ROI (Return on Investment) Rankings

ROI measures performance per dollar spent:

```
ROI = Category Score / Average Price per 1M tokens
```

Where:
```
Average Price = (Input Price + Output Price) / 2
```

Higher ROI indicates better value. A model with ROI of 5.0 delivers 5x more performance per dollar than a model with ROI of 1.0.

### Example

| Model | Coding Score | Avg Price | ROI |
|-------|--------------|-----------|-----|
| gpt-4o-mini | 0.454 | $0.19/1M | 2.42 |
| gpt-4o | 0.650 | $7.50/1M | 0.09 |

gpt-4o-mini provides 27x better value for coding tasks, despite lower absolute performance.

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
- **Gateway/aggregator providers**: OpenRouter, Portkey (incorrect pricing data)
- **Deprecated models**: Claude Instant, GPT-3.5, legacy snapshots
- **Meta/routing models**: Auto-routers, model mixtures

---

## Update Frequency

Rankings are regenerated weekly from fresh data sources. Benchmark scores are updated as new evaluations become available.
