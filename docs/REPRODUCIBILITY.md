# Reproducibility and visual sources

## Scope

This guide describes what is available in the committed project and what is required to reproduce it. The documentation update inspected source and saved outputs; it did not rerun model training or hardware/simulation experiments.

## Required inputs

Provide `english_cleaned.csv`, `kannada_cleaned.csv`, `malayalam_cleaned.csv`, and `tamil_cleaned.csv` under the configured `cleaned_data/` directory. Each requires `sentence` and `label` columns. Raw/cleaned datasets and pretrained/fine-tuned weights are not committed. Label meanings and dataset provenance must match your source data.

## Entry point

Create a Python environment with Jupyter, pandas, NumPy, scikit-learn, PyTorch, Transformers, tqdm, emoji, and the plotting libraries used in the notebooks. Select mutually compatible PyTorch/CUDA versions for your hardware.

Run the preprocessing notebook first, then open `xlmr_finetune (1).ipynb`. Replace `BASE_DIR` and other absolute paths before running cells. The Word2Vec-named notebook currently has the same content as preprocessing and is not a separate implemented Word2Vec baseline.

## Evidence and interpretation

The fine-tuning notebook configures a five-epoch run, cosine learning-rate scheduling, early stopping, and per-language evaluation. Its approximately 90% accuracy language is an improvement target, not a verified result. No completed benchmark summary or evaluation figure is included in this README because the inspected notebook outputs do not supply one.

## Visual provenance

All screenshots and experiment figures are tied to repository material. Workflow SVGs are explanatory illustrations. The full image inventory is in [assets/sources.json](assets/sources.json).

| Visual | Source |
| --- | --- |
| [overview.svg](assets/overview.svg) | New explanatory project-workflow diagram based on the committed source and documentation; not a screenshot or measured result. |

## Validation

```bash
python tools/check_docs.py
```

The standard-library checker validates README/docs local link destinations and SVG/PNG/JPEG headers. It makes no external requests and installs no project runtime dependencies. External web links, model accuracy, image semantics, and full application execution need separate review.

## Refresh notebook visuals

The exporter reads saved `image/png` outputs without executing notebook code:

```bash
python tools/export_notebook_images.py "xlmr_finetune (1).ipynb"
```

Review the exported images, remove any unsuitable or private content, choose the figures that explain the project, and update the README links and `docs/assets/sources.json`. It does not manufacture results when a notebook has no saved PNG output.

## Reproduction record

For a new experiment or demo, record the source commit, environment versions, data provenance and split, configuration, command/notebook order, and resulting artifacts. Only label a measurement as reproduced after completing that run. Keep credentials and restricted datasets outside version control.
