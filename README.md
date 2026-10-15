# nn — neural-net scratchpad notebooks

**Status: archive / deprecated (2021-2022 era) — kept for reference.**

A flat collection of ~50 throwaway Jupyter notebooks from hand-rolling neural
networks and attention from primitives in PyTorch (2021–2022 era). Nothing here
is a library, a product, or maintained code.

## Why it exists

Personal study/experiment log: implementing attention, self-attention,
trainer/eval loops, transfer, RL-style reinforcement, sparse PageRank, and
gradient-based image fitting directly against `torch.nn`, with no framework
above it. It was never structured as a library and has no entrypoint, tests, or
reproducible dataset. Kept as an archive of how the ideas were worked out.

## How to run

There is no supported way to run this as a project. The notebooks are
standalone and expect a CUDA GPU, local absolute paths from the original
machine, and (for the removed time-series notebook) a private backend. Run any
single notebook in Jupyter if you only want to read the code; most cells will
not execute outside the original environment. The image-fitting notebooks refer
to `assets/wallpaper2.png` and `assets/a.png`, and the imcopy notebooks to
`assets/a.png` — none of those local assets are shipped here.

## Status

Deprecated (2021–2022 era) — kept as an archive. Written against PyTorch 1.x
(`torch.set_default_tensor_type(torch.cuda.FloatTensor)`,
`torch.cuda.amp.GradScaler`) and Python 3.9/3.10; several APIs and the Dash
import style are deprecated by 2026. Notebook naming is `Untitled*` /
`*-Copy*`, so the set is not navigable without reading filenames first. Roughly
a third of the files are `Untitled*.ipynb` / `*-CopyN.ipynb` / `*.old.ipynb`
duplicates and dead ends.

## Sanitisation

This directory was migrated out of a private archive. The following were
removed or redacted before publication:

- a hard-coded RSA private key PEM block (now a
  `<REDACTED:rsa-private-key>` placeholder), its matching public key, and the
  cell that wrote the key to disk;
- `cov.ipynb`, which hard-coded a private time-series backend API token,
  endpoint, org, bucket, device identifier and sensor field names — the whole
  notebook was employer-internal, so it was removed rather than redacted;
- `dawn.yml`, an internal application/tenant schema;
- the employer-internal industrial sensor tag list and its MQTT mock publisher
  cells from `Untitled1.ipynb`, plus the `d:/bq/mqttmock/a.npz` path;
- owner-machine absolute paths (`D:/my/...`, `d:/a.png`, `d:/prv.pem`),
  replaced with neutral placeholders;
- the CIFAR-100 derived folders that `nnMeta/cnnTrainEval.ipynb` would
  re-export (not part of this directory).

No credentials, tokens, private keys, hostnames, or personal data are known to
remain. If you fork this, scan it yourself before publishing.

## License

AGPL-3.0-only; see `LICENSE`.
