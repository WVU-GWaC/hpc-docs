---
hide:
  - navigation
---

## Overview of Storage Offerings

Our data-storage offerings at GWaC are quite extensive, currently well over 2.5 Petabytes of "spinning" (ie: accessible) data. These systems all use a wide variety of protocols to optimize their desired use case, so its important to understand the structure of our offerings before running any compute jobs.

!!! note "An Aside on Data Storage Etiquette"
    These systems are shared by well over 100 active users, so it is important to practice proper data storage etiquette when using our offerings. We recommend reviewing ["Ten Simple Rules for Digital Data Storage"](https://doi.org/10.1371/journal.pcbi.1005097) (Hart et al, 2016) for a comprehensive guide on how to ensure your data is properly stored, categorized, and shared to increase collaborative productivity.

------


### Personal "Home" Storage

We currently offer users two tiers of storage when it comes to personal file storage on our resources. By default, all users have their `$HOME` (IE: `~/`) directory limited to a maximum size of 20 GB. This can be upgraded to a new maximum of 150 GB of storage should sufficient need be demonstrated to Site Administrators along with PI approval.

Due to the internal openness of our data services and size limitations, digital data stored at `$HOME` should be limited to:

- WIP code products;
- temporary file storage of small bespoke data-sets;
- personal work-related documents;
- and custom software / environments.

!!! note "For Legacy Users of Bowser"
​    Users whom previously used the Bowser HPC will find their old home directories located at `/bowser/`. These directories are readable by everyone, but are meant for fetching old data only and will be available until January 15th, 2023 when data will then be move to magnetic tape for long term storage.

------


### Compute Storage

Whenever a user wishes to submit a compute job to our HPC cluster, it is important to consider how their data will be read and written by the compute nodes assigned to the job. For example, the Lustre file system which provides our 1.4 PB storage array, `/hyrule/`, is not well optimized to read and then write lots of small files remotely. Instead, it is designed to safely store large data sets with lowered possibilities of "bit rot" and mechanical failures of the contained hard-disks.

As such, we provide all users of our **Link HPC** with a bit of computing **"scratch space"** located at `$SCRATCH` (colloquially, it is referred to as *Lorule*). This is an NFS mounted storage array with a total capacity of **~150 TB** in RaidZ-1. Connected over our high-bandwidth SAS, we regularly get about 575-676 MB/s of sustained read-write IO speeds. Currently, we do not have a limit for individual members. However, as a rule, nothing is backed up in `$SCRATCH` and can last for no longer than 6-months on these disks.

------


### WVU-Acquired Observatory Data

For projects where WVU is the leading institution, we have multiple storage options available. These are all located within the `/wvu/` directory on the **Link HPC**. A breakdown of currently available storage locations and their description follows:

!!! note "Regarding Environment Variables"

    Ensure that you have the `env/wvu` module file loaded via the command `module load env/wvu` to gain access to these environment variable short-cuts to various directories.

| Environment Variable&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Directory&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                 | Description                                                  | Total Limit | Currently Available |
| -------------------- | ------------------------- | ------------------------------------------------------------ | ----------- | ------------------- |
| `$GREENBANK`         | `/wvu/scopes/gbo`         | Primary storage for observational data transferred from the Green Bank Observatory (GBO) related to WVU-centric projects. | 211 TB      | 31 TB               |
| `$DRIFTSCAN`         | `/wvu/surveys/driftscan`  | Primary storage for the GBT 350-MHz Drift Scan Pulsar Survey [(Crowter et al, 2020)](https://doi.org/10.1093/mnras/staa933). | 134 TB        | 12 TB               |
| `$GREENBURST`        | `/wvu/surveys/greenburst` | Primary storage for the GreenBurst [(Surnis et al, 2019)](https://doi.org/10.1017/pasa.2019.26) FRB search survey for the GBT. | 67 TB       | 2.2 TB              |
| `$PSC_20M`           | `/wvu/scopes/20m`         | Auxiliary storage for data collected on the 20-meter telescope at Green Bank Observatory for the Pulsar Science Collaboratory. | 65 TB       | 1.6 TB              |



------


### NANOGrav-Acquired Observatory Data

For projects related to the NANOGrav PFC, we have one centeral storage offering, located at `/nanograv/` on the **Link HPC**. In principal, it is created from several JBODs all mounted within this central directory. A breakdown of currently available storage locations  and their description follows:

!!! note "Regarding Environment Variables"

    Ensure that you have the `env/nanograv` module file loaded via the command `module load env/nanograv` to gain access to these environment variable short-cuts to various directories.

| Environment Variable&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Directory&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                  | Description                                                  | Total Limit | Currently Available |
| -------------------- | -------------------------- | ------------------------------------------------------------ | ----------- | ------------------- |
| `$NANO_ARCHIVE`      | `/nanograv/archive/`       | Primary storage of all NANOGrav-related observational data.  | 390 TB      | 276 TB              |
| `$NANO_GBO`          | `/nanograv/archive/gbo`    | See above but specifically for [Green Bank Observatory](https://greenbankobservatory.org/) telescopes. | -           | -                   |
| `$NANO_CHIME`        | `/nanograv/archive/CHIME`  | See above, but specifically for the [CHIME](https://chime-experiment.ca/en) project. | -           | -                   |
| `$NANO_TIMING`       | `/nanograv/timing`         | Primary storage for all processed data for the NANOGrav Timing Working Group. | 78 TB       | 929 GB              |
| `$NANO_PROJECTS`     | `/nanograv/projects`       | Primary storage for various NANOGrav-lead projects.          | 40 TB       | -                   |
| `$NANO_SHARE`        | `/nanograv/share`          | Auxiliary storage for intermediate files necessary for a variety of on-going projects. | 3.7 TB      | -                   |
| `$NANO_NOTEBOOK`     | `/nanograv/notebook/homes` | Primary storage for `$HOME` / `~/` directories for the [NANOGrav Jupyter Notebook Server](notebook.nanograv.org) and their users. | 2.6 TB      | -                   |

------

### Moving Data from an Observatory to GWaC Storage

Due to security measures put in place in the Spring of 2022, all WVU machines can only be reached via SSH protocol (IE: `ssh`, `scp`, `rsync`, etc) through the dedicated SSH Gateway (`ssh.wvu.edu`). This requires Duo Two-Factor Authentication for all such opperations targetting WVU servers from remote machines. As such, it throws a bit of a wrench into what a normal user would do when transferring data from a remote site to their home institution.

We have included some basic solutions to specific use cases in the subsections below.

#### Transferring FROM a Remote Server TO GWaC Storage

Run the following command, replacing: `$WVU_USERNAME` with your WVU Username, `$LOCAL_FILE_LOCATION` with the absolute path to the files on the remote machine, and `$GWaC_FILE_LOCATION` with the absolute path of where the files will live at on GWaC Storage.
```bash
rsync -avz --progress -e "ssh $WVU_USERNAME@ssh.wvu.edu ssh" $LOCAL_FILE_LOCATION $WVU_USERNAME@link.phys.wvu.edu:$GWaC_FILE_LOCATION
```

#### Transferring FROM GWaC Storage TO a Remote Server
Run the following command, replacing: `$REMOTE_USERNAME` with your WVU Username, `$GWaC_FILE_LOCATION` with the absolute path of where the files live at on GWaC Storage, `REMOTE_SERVER_URL` with the remote server's URL, and `$REMOTE_FILE_LOCATION` with the absolute path to the where the files will be transferred to on the remote machine.
```bash
rsync -avz --progress -e $LOCAL_FILE_LOCATION $REMOTE_USERNAME@$REMOTE_SERVER_URL:$REMOTE_FILE_LOCATION
```


