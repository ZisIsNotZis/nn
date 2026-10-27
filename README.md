**English** | [简体中文](README.zh-CN.md)

<img src="assets/logo.svg" alt="nn" width="200">

# nn

Neural networks, attention and training loops written by hand on top of bare PyTorch — a 2021–2022 notebook archive.

**Fifty throwaway Jupyter notebooks that rebuild attention, a trainer/eval/transfer harness, sparse PageRank, image fitting and RL-style reinforcement from primitives, kept unedited as a record of how the ideas were worked out.**

There is no package, no entry point, no test suite and no dependency manifest here. This is a study log, not a library.

## Quick start

Requires Python with Jupyter and PyTorch installed. Clone and open any notebook to read or run it:

```bash
git clone https://github.com/ZisIsNotZis/nn.git
cd nn
jupyter lab attention/2d.ipynb
```

That is the whole supported workflow. Most cells will not execute outside the original machine: they call `torch.set_default_tensor_type(torch.cuda.FloatTensor)`, read image assets that are deliberately not shipped (`assets/`), and expect the original absolute paths. The imports across the tree are `torch`, `numpy`, `PIL`, `scipy`, `scikit-learn`, `matplotlib`, `tqdm`, `dash`/`plotly` and `rsa` — install only what the notebook you open actually needs.

## What is in here

- **From-scratch attention** — [`attention/1dpat.ipynb`](attention/1dpat.ipynb), [`attention/2d.ipynb`](attention/2d.ipynb), [`attention/2dpat.ipynb`](attention/2dpat.ipynb): `Attention`/scoring modules fit to a local image by gradient descent.
- **Self-attention** — [`SelfAttentionNn.ipynb`](SelfAttentionNn.ipynb), [`mlpSelfAttention.ipynb`](mlpSelfAttention.ipynb): a `SelfAttentionNn` module trained on a synthetic bit-unpacking classification task.
- **Trainer / eval / transfer harness** — [`nnMeta/nnTrainerEvaler.ipynb`](nnMeta/nnTrainerEvaler.ipynb), [`nnMeta/nnTransferer.ipynb`](nnMeta/nnTransferer.ipynb), `nnMeta/nnTrainEval*.ipynb`, `nnMeta/nnTreeTrainEval*.ipynb`: an evolving series of `%run`-driven experiment hosts built on `sklearn.datasets.make_classification`.
- **CNN on CIFAR-100** — [`nnMeta/cnnTrainEval.ipynb`](nnMeta/cnnTrainEval.ipynb): a `ConvBn`/`IterPool` stack fed from a local CIFAR-100 pickle folder.
- **Reinforcement as backprop** — [`reinforcer.ipynb`](reinforcer.ipynb): a `@reinforce` decorator that turns a plain function (add, multiply-mod-16) into a learned module and plots the result.
- **Sparse PageRank** — [`sparsePagerank.ipynb`](sparsePagerank.ipynb): power iteration on a 1M-node `scipy.sparse.coo_matrix`, with a threaded row-normalise step.
- **Gradient image fitting** — [`imcopy.ipynb`](imcopy.ipynb) and its copies: fit a low-resolution tensor to a target image and grow it (`LANCZOS`), plus [`Untitled4.ipynb`](Untitled4.ipynb) fitting a 1080p tensor directly.
- **Small Dash apps** — [`dash.ipynb`](dash.ipynb), [`dash-Copy1.ipynb`](dash-Copy1.ipynb): a key/value table editor and a rank demo, written against the pre-2.0 `dash_core_components` import style.
- **Scratch** — `Untitled*.ipynb`, `*-CopyN.ipynb`, `*.old.ipynb`, `testDebug.py`, `testDebug*.ipynb`: arithmetic doodles, timings and dead ends that were kept rather than pruned. `kv.json` is their ad-hoc key/value test data.

## Layout

```
.
├── attention/            attention and pattern modules fitted to images
├── nnMeta/               trainer/eval/transfer harness and the CIFAR-100 CNN
├── docs/project-status.md  classification, evidence, boundaries
├── *.ipynb               self-attention, reinforcement, PageRank, Dash, scratch
├── testDebug.py          the only .py file: eight lines of arithmetic
└── kv.json               test data for the Dash key/value notebook
```

Every notebook is standalone and top-level — none import each other and there is no shared module. The pieces "talk" only through the ideas they repeat: a `Nn`/`Module` built on `torch.nn`, an `Adam` + `OneCycleLR` training loop, and a plotting cell at the end. The `nnMeta` series re-declares an earlier notebook's harness with one thing changed; that lineage is the point of the archive, not a refactor that was abandoned halfway.

## Development

Nothing to build, install or lint, and no tests to run: the tree contains no package metadata, no CI configuration and no dependency manifest. The working method was:

1. Open a notebook next to the notebook it forked from.
2. Edit the module or the task in place (usually the loss, the scheduler or the sample shape).
3. Run the training loop, look at the plot, keep the file if the result was interesting.

New work is not tracked here — the archive is frozen and untested; see [`docs/project-status.md`](docs/project-status.md) for what each cluster of files was and where the boundaries are.

## Contributing

Fixes to broken links, redactions or factual documentation are welcome — open an issue or a PR with the smallest change that makes the correction. Do not send notebook refactors, reformatting or new experiments; the value of this directory is that the old cells are untouched.

If you fork or republish this, **scan it yourself first** and read the sanitisation notes below.

## Roadmap

**Implemented** — everything listed under "What is in here", as notebooks. Several of these are the complete version of an idea: `SelfAttentionNn.ipynb` trains attention end to end, `sparsePagerank.ipynb` converges on a million-node graph, `reinforcer.ipynb` learns both of its toy tasks.

**Planned** — nothing. This is a closed archive, not a project under construction; no notebook will be promoted to a library, unified behind a single entry point, or ported to a current PyTorch. The realistic future is continued read-only hosting: the notebooks stay as a record of hand-rolling these mechanisms before reaching for a framework, and any successor work lives in a different repository.

## Sanitisation

This directory was migrated out of a private archive. The following were removed or redacted before publication:

- a hard-coded RSA private key PEM block (now a `<REDACTED:rsa-private-key>` placeholder), its matching public key, and the cell that wrote the key to disk;
- `cov.ipynb`, which hard-coded a private time-series backend API token, endpoint, org, bucket, device identifier and sensor field names — it was employer-internal, so it was removed rather than redacted;
- `dawn.yml`, an internal application/tenant schema;
- the employer-internal industrial sensor tag list and its MQTT mock publisher cells from `Untitled1.ipynb`, plus the `d:/bq/mqttmock/a.npz` path;
- owner-machine absolute paths (`D:/my/...`, `d:/a.png`, `d:/prv.pem`), replaced with neutral placeholders;
- the CIFAR-100 derived folders that `nnMeta/cnnTrainEval.ipynb` would re-export (not part of this directory).

No credentials, tokens, private keys, hostnames, or personal data are known to remain.

## License

AGPL-3.0-only; see [`LICENSE`](LICENSE). Copyright ZisIsNotZis.
