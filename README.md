# Connectome-constrained Drosophila Decoder

A leaky integrate-and-fire model of the adult *Drosophila* brain, constrained by
the FlyWire connectome. Activates or silences sets of neurons by FlyWire ID and
reads out the resulting spike times and rates. The underlying simulator lives in
the [`Drosophila_brain_model`](https://github.com/philshiu/Drosophila_brain_model)
submodule (Shiu et al., bioRxiv 2023.05.02.539144).

## Quickstart

Requires [uv](https://docs.astral.sh/uv/) and Python 3.10.

```bash
# Clone with the model submodule
git clone --recurse-submodules <repo-url>
cd drosophila

# Or, if already cloned
git submodule update --init --recursive

# Create the environment and install dependencies
uv sync

# Run
uv run python main.py
```

The environment pins `setuptools<81` and `cython<3` so that brian2 2.5.1 builds
its C++ code generation backend correctly.

To explore interactively, launch Jupyter and open the bundled tutorial notebook:

```bash
uv run jupyter lab Drosophila_brain_model/example.ipynb
```

## Repo layout

```
.
├── main.py                  # Entry point
├── pyproject.toml           # Project metadata and pinned dependencies
├── uv.lock                  # Resolved dependency lockfile
├── papers/                  # Reference papers
└── Drosophila_brain_model/  # Upstream model (git submodule)
    ├── model.py             # LIF model: create_model, run_exp, run_trial
    ├── utils.py             # Loading and rate helpers: load_exps, get_rate
    ├── example.ipynb        # Tutorial notebook
    ├── figures.ipynb        # Paper figure reproduction
    ├── Connectivity_783.parquet     # Connectome (synaptic connectivity)
    ├── Completeness_783.csv         # Per-neuron completeness metadata
    └── results/example/     # Example simulation outputs
```
