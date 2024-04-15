# Creating a conda/mamba environment

[conda](https://docs.conda.io/projects/conda/en/stable/) and
[mamba](https://github.com/mamba-org/mamba) are software environment
management commands that let you install and execute software in your
own account without any special access. With conda/mamba you can:

* install your own command-line software
* install specific versions of R and Python, as well as Python and R packages
* create "clean" environments that contain only a specific set of software
* "pin" versions of software to ensure reproducibility

Most data science software is available via conda.

conda and mamba are available on farm via the `module` command. The following
will enable both the `conda` and `mamba` commands:
```
module load mamba
```

Conda is the simplest way to use your own installation of R and R packages
with RStudio Server, and Python and Python packages with JupyterLab.
See below for details!

References and tutorials:

* [Installing software on remote computers with conda/mamba](https://hackmd.io/BffW5KHxTCKPyhUAo2tqHg?view) - from GGG 298/Tools for Data Intensive Research, WQ 2023/2024.

## Creating a conda environment for RStudio Server

If you want to run RStudio via Open OnDemand with a specific version
of R and install your own packages in RStudio, you can do that with
conda by creating a conda environment that contains the
[`r-base` package from conda-forge](https://anaconda.org/conda-forge/r-base/files). This
will provide the `R` command. You can also install any additional
packages you are interested in using, e.g. `dplyr` via
[the `r-dplyr` package](https://anaconda.org/conda-forge/r-dplyr/files).

For example, if you run this on the command line, this command:
```shell
mamba create -y -n my-r-env r-base=4.2.3 r-dplyr
```
will create a conda environment named `my-r-env` that contains R v4.2.3
along with a compatible version of dplyr.

To run RStudio with this version of R, specify `my-r-env` in the conda
environment configuration when starting RStudio via Open OnDemand.

Note that this environment is entirely isolated from others! So you
need to install everything you are going to use in RStudio in this
conda environment, even if it's installed elsewhere in your
account. You can do so by installing it with conda, or you can install
packages directly with `install.packages()` or your usual R
installation mechanisms.

## Creating a conda environment for JupyterLab

If you want to run your own Python version, with its own package installs,
in JupyterLab via Open OnDemand, you'll need to install your own Python
["kernel"](https://docs.jupyter.org/en/latest/projects/kernels.html). This
can be done with conda quite easily!

For example, the following commands will create a conda environment with
Python v3.12, and install it as a Jupyter kernel:
```
mamba create -n py312 -y python=3.12 ipykernel
mamba activate py312
python -m ipykernel install --user --name py312
```

To use this version of Python in JupyterLab, select the `py312` kernel
when starting a notebook, or select the kernel from the Kernel
... Change Kernel menu.

Note that this environment is entirely isolated from others! So you
need to install everything you are going to use in Jupyter in this
conda environment, even if it's installed elsewhere in your
account. You can do so by installing it with conda/mamba, or you can
install packages via your usual Python installation mechanisms
(e.g. `python -m pip`).  You'll need to run the install commands in the
`py312` conda environment.
