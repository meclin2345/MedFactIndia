# MedFactIndia: A Benchmark for Grading Health Misinformation Severity from Indian Fact-Checking Sources

This repository provides the official dataset, baseline predictions, and replication code for the paper:
**"MedFactIndia: A Benchmark for Grading Health Misinformation Severity from Indian Fact-Checking Sources"**.

## Repository Structure
- `medfactindia.csv`: The complete benchmark corpus of 2,745 fact-checked health claims paired with expert medical explanations and metadata.
- `data_splits/`: Standard 70/15/15 label-stratified splits (train, dev, test).
- `grouped_split/`: Leak-free cluster-stratified splits partitioned by near-duplicate claim connected components.
- `predictions/`: Pre-computed prediction CSVs for all 33 experimental runs (fine-tuned encoders across seeds 42, 43, 44 and prompted LLMs).
- `reviewer_analyses.py`: Tool for duplicate leakage auditing, subset re-evaluation, and verdict-family analysis.
- `experiments.ipynb`: Training and evaluation notebook for transformer baselines.
- `results_analysis/`: Aggregate baseline tables and bootstrap confidence interval summaries.
- `annotation/`: Human validation annotation sample sheets and unblinded keys.

## Quick Start
To reproduce the overlap audit and novel test subset evaluation:
```bash
# Run overlap audit
python reviewer_analyses.py overlap --train data_splits/train.csv --dev data_splits/dev.csv --test data_splits/test.csv --out overlap_test.csv

# Re-score predictions on low-overlap subset
python reviewer_analyses.py eval-subset --test data_splits/test.csv --overlap overlap_test.csv --preds predictions/ --threshold 0.8
```

## License
Released under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license.
