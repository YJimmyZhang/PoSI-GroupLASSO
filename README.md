# PoSI-GroupLASSO
Post-selection Inference for Group Lasso Penalized M-Estimators

This is a fork of [yiling-h/PoSI-GroupLASSO](https://github.com/yiling-h/PoSI-GroupLASSO). The code is unchanged. The original no longer installs with current package versions, so I pinned the setup to the versions it was developed with. See [Changes](#changes) below.

## Installation
Tested on macOS with Python 3.10.

I used [uv](https://docs.astral.sh/uv/) to set up the environment, because it installs Python 3.10 itself. Install it first:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

On Windows, see the uv website for the install command.

Then:

```bash
git clone https://github.com/YJimmyZhang/PoSI-GroupLASSO.git
cd PoSI-GroupLASSO
uv venv --python 3.10 --managed-python .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
uv pip install numpy==1.23.4 cython setuptools
uv pip install -r requirements-working.txt --no-build-isolation
```

To check that it works:

```bash
python -m selectinf.Simulation.gaussian_simulation 0 2
```

This runs 2 replications and writes two CSV files to the repo folder.

I haven't tested this on Windows. `regreg` has to be compiled during installation, so on Windows you may need the [Microsoft C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/).

## Changes
No changes to the code. Only the setup:
- **Python 3.10 and NumPy 1.23.4.** These are the versions used in the original (see the earlier `requirements.txt` and the notebooks). Newer NumPy versions break the code: NumPy 1.24 removed `np.bool` and `np.float`, and `regreg` doesn't build with NumPy 2.
- **`regreg` installed with `--no-build-isolation`.** It needs Cython to build but doesn't list it as a build requirement, so Cython is installed first.
- **Added `seaborn` and `matplotlib`.** They are imported but were missing from `requirements.txt`.
- **Added `requirements-working.txt`** with the exact package versions I used, including `regreg` at commit `beb3630`.

## Potential Issues & Solutions
1. We used the Poisson regression functionality in `regreg` to solve for certain parameters in simulations for Poisson regression. The original `regreg` code requires integer responses, which may not be the case in our simulation setup. In these cases `regreg` stops with an error asking for an integer response. This can be solved by commenting out lines 1048 and 1049 in `.venv/lib/python3.10/site-packages/regreg/smooth/glm.py`.

## Related Paper & Replicability
1. The corresponding paper with theoretical results can be found at [link to paper](https://arxiv.org/pdf/2306.13829.pdf).
2. To replicate the simulation section, see the following files under `selectinf/Simulation`:
   1. Gaussian link: `gaussian_simulation.py`
   2. Logistic link: `logistic_simulation.py`
   3. Poisson link: `poisson_simulation.py`
   4. Quasi-Poisson modeling for negative binomial responses: `quasipoisson_simulation.py`
3. An interactive Jupyter Notebook that runs small-scale replications of all four experiments is at `selectinf/Replicability/replication_tutorial.ipynb`.

## Troubleshooting
For issues with the original code, contact Yiling Huang (yilingh@umich.edu).