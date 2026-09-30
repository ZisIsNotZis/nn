# nn project status

## Classification

Archive: a flat collection of ~50 throwaway Jupyter notebooks from hand-rolling
neural networks and attention from primitives in PyTorch (2021–2022 era). Not
standalone tooling — a personal study/experiment log. There is no package, no
entrypoint, no test suite, and no dependency manifest anywhere in the tree.

## Status

Archive / deprecated (2021-2022 era) — kept for reference. Written against
PyTorch 1.x (`torch.set_default_tensor_type(torch.cuda.FloatTensor)`,
`torch.cuda.amp.GradScaler`) and Python 3.9/3.10. Several APIs and the
`dash_core_components` / `dash_html_components` import style are deprecated by
2026. About a third of the files are `Untitled*` / `*-CopyN*` / `*.old`
duplicates and dead ends. Sanitised for publication (see README).

## Evidence

- `SelfAttentionNn.ipynb` — defines a `SelfAttentionNn` module and a synthetic
  bit-unpacking classification task, built directly on `torch.nn`.
- `attention/2d.ipynb`, `attention/2dpat.ipynb`, `attention/1dpat.ipynb` —
  from-scratch `Attention` / scoring modules, fit to a local image by gradient
  descent; `1dpat.ipynb` also carries the (now redacted) RSA key detour.
- `nnMeta/nnTrainerEvaler.ipynb`, `nnMeta/nnTransferer.ipynb`,
  `nnMeta/nnTreeTrainEval*.ipynb`, `nnMeta/nnTrainEval*.ipynb` — a
  trainer/eval/transfer harness series.
- `reinforcer.ipynb`, `sparsePagerank.ipynb`, `mlpSelfAttention.ipynb` — RL-style
  reinforcement, sparse PageRank, and MLP+attention experiments.
- `dash.ipynb`, `dash-Copy1.ipynb` — small Dash apps (per-file key/value table;
  rank demo), written against the pre-2.0 Dash import style.
- `testDebug.py`, `testDebug*.ipynb` — 8-line arithmetic doodles; `kv.json` is
  ad-hoc key/value test data (GBK-encoded).

## Boundaries

No supported way to run this as a project: the notebooks expect a CUDA GPU,
the original machine's absolute asset paths (replaced with placeholders here),
and, for the removed notebook, a private time-series backend whose hard-coded
API token was exposed in the private archive and must be treated as compromised
and rotated. No executed outputs are present (every cell has empty outputs);
two pasted loss-plot image attachments remain and were inspected for
credentials, hostnames, and personal data. `nnMeta/cnnTrainEval.ipynb`
consumes the public CIFAR-100 dataset from a relative `../dat/` path; those
derived folders are not shipped. No LICENSE file — all rights reserved by the
author until a license is chosen.
