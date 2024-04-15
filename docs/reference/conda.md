# Creating a conda/mamba environment

## Creating a conda environment for RStudio Server

...to provide your own version of R + R packages

## Creating a conda environment for JupyterLab

Use [conda](https://docs.conda.io/projects/conda/en/stable/) or [mamba](https://github.com/mamba-org/mamba) to keep your python environments separate. We'll show `conda` here, but `mamba` uses the same syntax so everything applies if you'd rather use it.

First you need to load up the `conda` module:

`module load conda`

You can create an environment with the name `myjupyterenv` by calling:

`conda create -n myjupyterenv <optional packages to install>`

After this process has finished, you can _activate_ the virtual environment by calling: 

`conda activate myjupyterenv`. 

For example, to install JupyterLab from the `conda-forge` channel and you could use the following commands:

```
conda create -n myjupyterenv jupyterlab -c conda-forge
conda activate myjupyterenv  # activate our environment
```

Once an environment is activated, `conda install` can be used to install further packages into the environment.

### Tips

If you are creating a script to run with `sbatch`/`srun`, add `module load conda` and `conda activate <yourenv>` to the top to make sure your env is all ready to go.

To create a new jupyter kernel based on a conda env: Run `python -m ipykernel install --user --name=<myenv>` where `<myenv>` is the name of the environment.
