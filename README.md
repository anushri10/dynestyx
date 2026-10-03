# Structured Continuous-Discrete SLGSSMs for Multi-Agent Interactions

Here we provide all code to reproduce results in **“Structured Continuous-Discrete Switching Linear Gaussian State-Space Models for Multi-Agent Interactions,”**.

The paper introduces a structured continuous-discrete switching linear Gaussian state-space model for recovering regime-dependent interactions from partially and irregularly observed multi-agent trajectories. The latent state contains each agent’s position and velocity, while regime-dependent interaction weights define interpretable cross-agent coupling.

This work is implemented in a fork of [Dynestyx](https://github.com/BasisResearch/dynestyx). 

## Main Result Notebook

The complete simulation study is provided in:

- [`SLDS_mutli_agent_model.ipynb`](docs/tutorials/gentle_intro/SLDS_mutli_agent_model.ipynb)

The notebook includes:

- simulation from the structured position-velocity SLDS;
- MAP estimation using a point-mass variational approximation and a Rao-Blackwellized particle filter;
- parameter and filtered-state recovery under uniform and empirically derived missing-observation patterns; and
- parameter and filtered-state recovery under independently generated irregular observation schedules.

## Saved results

The numerical results used by the notebook are included so that the figures can be regenerated without rerunning model fitting:

- [`SLDS_mutli_agent_model_recovery_results.npz`](docs/tutorials/gentle_intro/SLDS_mutli_agent_model_recovery_results.npz): parameter and filtered-state recovery under regular-grid masking and missing observations.
- [`SLDS_mutli_agent_model_irregular_recovery_results.npz`](docs/tutorials/gentle_intro/SLDS_mutli_agent_model_irregular_recovery_results.npz): parameter and filtered-state recovery across irregular observation schedules.

## Implementation

The branch includes the SLDS and missing-observation functionality required by the experiments. The principal implementation files are:

- [`dynestyx/inference/integrations/cd_dynamax/discrete_filter.py`](dynestyx/inference/integrations/cd_dynamax/discrete_filter.py)
- [`dynestyx/inference/configs/filter.py`](dynestyx/inference/configs/filter.py)
- [`dynestyx/inference/filters.py`](dynestyx/inference/filters.py)
- [`dynestyx/models/state_evolution.py`](dynestyx/models/state_evolution.py)
- [`dynestyx/models/observations.py`](dynestyx/models/observations.py)
- [`dynestyx/distributions.py`](dynestyx/distributions.py)

The corresponding implementation tests are in [`tests/test_slds_rbpf.py`](tests/test_slds_rbpf.py) and [`tests/test_missing_observations.py`](tests/test_missing_observations.py).

## Environment setup

Clone this branch and install the development environment using [`uv`](https://docs.astral.sh/uv/):

```bash
git clone --branch neurips-2026-reproducibility \
    https://github.com/anushri10/dynestyx.git
cd dynestyx
uv sync --group dev
```

Start Jupyter from the repository root:

```bash
uv run jupyter lab docs/tutorials/gentle_intro/SLDS_mutli_agent_model.ipynb
```

The full recovery experiments use the fixed random seeds and settings specified in the notebook and may require substantial computation. The included `.npz` archives can be loaded by the plotting cells without rerunning model fitting.

## Empirical missingness patterns

The synthetic uniform-missingness and irregular-sampling experiments are documented by the notebook and saved result files. Cells that construct observation masks from the empirical dataset additionally require `train.npz`, `val.npz`, and `test.npz`. Set their parent directory before running those cells:

```bash
export DYNESTYX_SLDS_DATA_DIR=/absolute/path/to/data
```

The empirical dataset is not redistributed in this repository.

## Upstream project

For the maintained Dynestyx package, documentation, and general tutorials, see the [upstream Dynestyx repository](https://github.com/BasisResearch/dynestyx). Links to the upstream implementation will be added here as the relevant changes are integrated.

## Citation

Citation information for the workshop paper will be added when the proceedings metadata is available.

## License

This branch retains the license of the upstream Dynestyx project. See [`LICENSE.md`](LICENSE.md).
