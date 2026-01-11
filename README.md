# LLM Models

An open source of truth for Large Language Model data.

## Goals

### 1. Comprehensive & Up-to-Date

The AI landscape changes weekly. New models launch, prices drop, capabilities evolve.

- **100+ providers** crawled for model data
- **Weekly updates** to catch new releases and price changes
- **11,000+ models** tracked with specs, pricing, and capabilities

Staying current means you always have accurate data for decision-making.

### 2. Unbiased Assessments

Most model comparisons are biased. Providers highlight benchmarks where they excel. Marketing cherry-picks favorable metrics. Leaderboards weight benchmarks arbitrarily.

Our approach:
- **Equal weighting** for all benchmarks within each category
- **No cherry-picking** - every benchmark counts the same
- **Transparent methodology** - simple averaging, fully auditable

A model can't game rankings by excelling at one metric. Broad capability is required.

### 3. All Evaluations

We crawl benchmark data from multiple authoritative sources:

- **[Epoch AI](https://epoch.ai)** - GPQA, SWE-bench, MATH, MMLU, and more
- **[LMSys Arena](https://lmarena.ai)** - Human preference ELO from millions of votes
- **[LiveBench](https://livebench.ai)** - Contamination-free benchmarks
- **Official announcements** - Provider-reported scores

Combined with pricing from official API pages, this enables both performance rankings and ROI (value per dollar) analysis.

## Top Models (January 2026)

| Category | #1 | #2 | #3 |
|----------|-----|-----|-----|
| **Arena ELO** | Gemini 3 Pro | Gemini 3 Flash | Claude Opus 4.5 |
| **Coding (SWE-bench)** | Claude Opus 4.5 | Claude Sonnet 4.5 | gpt-5 |
| **Reasoning** | Gemini 3 Pro | o3 | o3-mini |
| **Hard/Frontier** | Gemini 3 Pro | Gemini 3 Flash | o3-mini |
| **ROI: Coding** | gpt-5-nano | DeepSeek V3 | gpt-5-mini |

*Full rankings: [docs/rankings.md](docs/rankings.md)*

## Quick Stats

| Metric | Count |
|--------|-------|
| Providers | 108 |
| Total Models | 11,757 |
| With Pricing | 1,586 |
| With Benchmarks | 1,211 |

## What's Included

| Directory | Contents |
|-----------|----------|
| `rankings/` | JSON rankings for each category |
| `csv/` | CSV exports of all rankings |
| `providers/` | Per-provider model data |
| `data/` | Combined model data and statistics |
| `docs/` | Methodology and documentation |

## Documentation

- [Methodology](docs/methodology.md) - How rankings are calculated
- [Rankings](docs/rankings.md) - All ranking categories with links to data

## Using the Data

All data is available in JSON and CSV formats:

```python
import json

# Load all models
with open('data/all_models.json') as f:
    data = json.load(f)
    print(f"Total models: {data['total_models']}")

# Load coding rankings
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
