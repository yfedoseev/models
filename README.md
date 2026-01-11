# LLM Models

An open database of Large Language Models: specs, pricing, and benchmarks from 100+ providers.

## Goals

### 1. Comprehensive & Up-to-Date

The AI landscape changes weekly. New models launch, prices drop, capabilities evolve.

- **100+ providers** crawled for model data
- **Weekly updates** to catch new releases and price changes
- **11,000+ models** tracked with specs, pricing, and capabilities

Staying current means you always have accurate data for decision-making.

### 2. Primary Benchmark Rankings

Most model comparisons are biased. Providers highlight benchmarks where they excel. Marketing cherry-picks favorable metrics. Easy benchmarks (HumanEval: 90%+ common) get equal weight to hard ones (SWE-bench: 80% is exceptional).

Our approach:
- **Primary benchmark ranking** - each category has a primary benchmark that determines rank
- **Hard benchmarks first** - models with hard benchmarks always rank above models with only easy ones
- **Transparent methodology** - see [docs/methodology.md](docs/methodology.md)

| Category | Primary Benchmark | Why |
|----------|------------------|-----|
| Coding | SWE-bench Verified | Real GitHub issues, not toy functions |
| Reasoning | GPQA Diamond | PhD-level science, not trivia |
| Knowledge | SimpleQA Verified | Factual accuracy, hard for LLMs |

A model can't rank high by acing easy benchmarks. Real-world capability is required.

### 3. All Evaluations

We crawl benchmark data from multiple authoritative sources:

- **[Epoch AI](https://epoch.ai)** - GPQA, SWE-bench, MATH, MMLU, and more
- **[LMSys Arena](https://lmarena.ai)** - Human preference ELO from millions of votes
- **[LiveBench](https://livebench.ai)** - Contamination-free benchmarks
- **Official announcements** - Provider-reported scores

Combined with pricing from official API pages, this enables both performance rankings and ROI (value per dollar) analysis.

## Top Models (January 2026)

### Performance Rankings

| Category | #1 | #2 | #3 |
|----------|-----|-----|-----|
| **Arena ELO** | Gemini 3 Pro | Gemini 3 Flash | Claude Opus 4.5 |
| **Coding** | Claude Opus 4.5 | Claude Sonnet 4.5 | GPT-5.1 Codex |
| **Reasoning** | Gemini 3 Pro | o3-mini | o3 |
| **Knowledge** | Gemini 3 Pro | Qwen3 Max | Gemini 3 Flash |
| **Hard/Frontier** | o4-mini | o3-mini | o3 |

### ROI Rankings (Best Value)

| Category | #1 | #2 | #3 |
|----------|-----|-----|-----|
| **ROI: Coding** | gpt-5-nano | Qwen3-235B | Qwen3-32B |
| **ROI: Reasoning** | Llama-3.2-11B | gpt-5-nano | Llama-3-8B |
| **ROI: Knowledge** | Llama-3-8B | Llama-3.2-11B | gpt-5-nano |
| **ROI: Hard** | o4-mini | o3-mini | o3 |
| **ROI: Arena** | Llama-3.1-8B | Gemma-3-4B | Gemma-2-2B |

*Full rankings: [docs/rankings.md](docs/rankings.md)*

## Quick Stats

| Metric | Count |
|--------|-------|
| Providers | 108 |
| Total Models | 11,481 |
| With Pricing | 1,578 |
| With Benchmarks | 1,222 |

## What's Included

### Model Data
Each model includes (where available):
- **Specs**: Context window, max output tokens, modalities
- **Pricing**: Input/output cost per million tokens
- **Benchmarks**: 30+ evaluations (SWE-bench, GPQA, Arena ELO, etc.)

### Directory Structure

| Directory | Contents |
|-----------|----------|
| `providers/` | Per-provider model data (JSON) |
| `data/` | Combined model database and statistics |
| `rankings/` | Performance rankings by category |
| `csv/` | CSV exports of all data |
| `docs/` | Methodology and documentation |

## Documentation

- [Methodology](docs/methodology.md) - How rankings are calculated
- [Rankings](docs/rankings.md) - All ranking categories with links to data

## Using the Data

All data is available in JSON and CSV formats:

```python
import json

# Load all models from a provider
with open('providers/openai.json') as f:
    openai = json.load(f)
    for model in openai['models'][:3]:
        print(f"{model['name']}: ${model.get('input_price_per_million', 'N/A')}/1M input")

# Load combined model database
with open('data/all_models.json') as f:
    data = json.load(f)
    print(f"Total models: {data['total_models']}")

# Load rankings
with open('rankings/coding.json') as f:
    coding = json.load(f)
    for model in coding['models'][:5]:
        print(f"{model['rank']}. {model['name']}: {model['score']}")
```

## Contributing

Found incorrect data? Prices changed? New model missing?

Open an issue or submit a PR with the correction and source.

## License

MIT License - see [LICENSE](LICENSE)
