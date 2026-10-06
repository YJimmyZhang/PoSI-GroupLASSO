# PoSI-GroupLASSO
Post-selection Inference for Group Lasso Penalized M-Estimators

## Installation

Tested with Python 3.11 on macOS 26. Requires `uv` (https://docs.astral.sh/uv/).

```bash
git clone https://github.com/YJimmyZhang/PoSI-GroupLASSO.git
cd PoSI-GroupLASSO
uv venv --python 3.11 --managed-python .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
uv pip install "numpy<2" cython setuptools
uv pip install -r requirements-working.txt --no-build-isolation
```

Check:

```bash
python -c "import regreg, selectinf; print('ok')"
python -m selectinf.Simulation.gaussian_simulation 0 2
```

## Potential Issues & Solutions
1. We used the Poisson regression functionality in `regreg` to solve for certain parameters
in simulations for Poisson regression, the original `regreg` codes require integer responses,
which may not be the case in our simulation setup. 
In these occasions, the original `regreg` file will produce an error message prompting for an
integer response and stop running, which can be solved by commenting out lines 1048 and 1049
in env3/lib/python3.10/site-packages/regreg/smooth/glm.py
2. Due to package compatibility, a python version >= 3.10 is recommended for the virtual environment.

## Related Paper \& Replicability
1. The corresponding paper with theoretical results can be found at [link to paper](https://arxiv.org/pdf/2306.13829.pdf).
2. To replicate the simulation section, one can refer to the following files under the path `selectinf/Simulation`:
   1. Gaussian link: `gaussian_simulation.py`
   2. Logistic link: `logistic_simulation.py`
   3. Poisson link: `logistic_simulation.py`
   4. Quasi-Poisson modeling for negative binomial responses: `quasipoisson_simulation.py`
3. An interactive Jupyter Notebook that runs small scale replications of all four experiments is given at
`selectinf/Replicability/replication_tutorial.ipynb`. 
To run the Jupyter Notebook using the virtual environment `env3` created earlier, 
it is recommended to open the project using a Python IDE such as PyCharm.

## Troubleshooting
For potential issues and mistakes, please contact Yiling Huang (yilingh@umich.edu) for correction.
