## Overview of Storage Offerings

Our data-storage offerings at GWaC are quite extensive, currently well over 2.5 Petabytes of "spinning" (ie: accessible) data. These systems all use a wide variety of protocols to optimize their desired use case, so its important to understand the structure of our offerings before running any compute jobs.

!!! note "An Aside on Data Storage Etiquette"
    These systems are shared by well over 100 active users, so it is important to practice proper data storage etiquette when using our offerings. We recommend reviewing ["Ten Simple Rules for Digital Data Storage"](https://doi.org/10.1371/journal.pcbi.1005097) (Hart et al, 2016) for a comprehensive guide on how to ensure your data is properly stored, categorized, and shared to increase collaborative productivity.

### Personal "Home" Storage

We currently offer users two tiers of storage when it comes to personal file storage on our resources. By default, all users have their `$HOME` (IE: `~/`) directory limited to a maximum size of 20 GB. This can be upgraded to a new maximum of 150 GB of storage should sufficient need be demonstrated to Site Administrators along with PI approval. 

Due to the internal openness of our data services and size limitations, digital data stored at `$HOME` should be limited to:

- WIP code products;
- temporary file storage of small bespoke data-sets;
- personal work-related documents;
- and custom software / environments.

### Compute Storage

Whenever a user wishes to submit a compute job to our HPC cluster, it is important to consider how their data will be read and written by the compute nodes assigned to the job. For example, the Lustre file system which provides our 1.4 PB storage array, `/hyrule/`, is not well optimized to read and then write lots of small files remotely. Instead, it is designed to safely store large data sets with lowered possibilities of "bit rot" and mechanical failures of the contained hard-disks.

As such, we provide all users of our **Link HPC** with a bit of computing **"scratch space"** located at `$SCRATCH` (colloquially, it is referred to as *Lorule*). This is an NFS mounted storage array with a total capacity of **~150 TB** in RaidZ-1. Connected over our high-bandwidth SAS, we regularly get about 575-676 MB/s of sustained read-write IO speeds. Currently, we do not have a limit for individual members. However, as a rule, nothing is backed up in `$SCRATCH` and can last for no longer than 6-months on these disks. 

### WVU-Acquired Observatory Data

For projects where WVU is the leading institution, we have multiple storage options available. These are all located within the `/wvu/` directory on the **Link HPC**. A breakdown of currently available storage locations and their description follows:

### NANOGrav-Acquired Observatory Data

For projects related to the NANOGrav PFC, we have one centeral storage offering, located at `/nanograv/` on the **Link HPC**. In principal, it is created from several JBODs all mounted within this central directory. A breakdown of currently available storage locations  and their description follows:

