---
hide:
  - navigation
---

## For Pulsar-Related Science ...

Once connected to **Link HPC** using your WVUID, you will need to edit your `~/.bash_profile` file. 

However, to make things easy on our users, we have created a script which will automatically set up your default shell environment for pulsar-related science.

You can activate this script by running the following command (DO NOT ADD THIS TO YOUR `~/.bashrc` or `~/.bash_profile`; SIMPLY RUN THE COMMAND FROM TERMINAL):

``` shell
source /scripts/SetUp_PulsarEnv.sh
```

??? Walkthrough of How the Environment is Set-Up

    You can do this either through SSH using your favorite command-line text editor (`vim`, `nanon`, etc) **-OR-** via the text editor on the OnDemand Web Interface. Regardless of your editing preference, you need to add the following lines to your environment:

    ``` shell
    module load openmpi/4.1.4 python/3.9 pulsar
    ```

    You then need to either restart your Shell session **-OR-** run the following via the command-line:

    ``` shell
    source ~/.bash_profile
    ```

    After your environment has been modified correctly, you will then need to run:

    ``` shell
    conda init
    ```

    This will load the pre-installed version of Anaconda located at `/opt/miniconda3/` and allow you to start using `conda` controlled environments.

    To use the pre-installed pulsar python packages, please run the following command:

    ``` shell
    conda activate pulsar
    ```

    This will set your current `conda` environment from the `(base)` environment to `(pulsar)`, which has several scientific packages pre-installed and optimized for our cluster's environment.

    If you want to make this permanent, you need to add the above command to the end of your `~/.bash_profile`. You can do this by running:

    ``` shell
    echo 'conda activate pulsar' >> ~/.bash_profile
    ```



Should you need to do any development work, you can create your own environment using the following commands:

```
conda deactivate
conda create --name ${USER} --clone pulsar
conda activate ${USER}
```

This will:

- deactivate the `pulsar` environment

- create your own personal `conda` environment (located in ~/.conda/envs/${USER}) which is a clone of `pulsar`

- activate your personal `conda` environment.

The name of this environment will be your User Name.

!!! Note "Mamba vs Conda"
    We use `mamba` in place of `conda` here as it speeds up the process of installing Anaconda packages dramatically. Whenever you need to install packages, please use `mamba install` rather than `conda install`. You can find more information here: https://mamba.readthedocs.io/en/latest/
