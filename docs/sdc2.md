# SKA Science Data Challenge 2

The IAA-CSIC proto-SRC has offered computing resources for the 2nd SKA Science Data Challenge (SDC2).
For more information on how to participate visit:

[https://sdc2.astronomers.skatelescope.org](https://sdc2.astronomers.skatelescope.org)

If your team has been allocated to the IAA-CSIC proto-SRC resource, please email ska-itsupport 'at'
iaa.csic.es to get access.

# Virtual machine flavors

Here we show the flavors offered for the SDC2:

| Flavor Name  | vCPUs | RAM    | Root Disk | Additional block storage |
|:------------:|:-----:|:------:|:---------:|:------------------------:|
| sdc2.c16m64  | 16    | 64 GB  | 100 GB | 2 TB |
| sdc2.c32m128 | 32    | 128 GB | 100 GB | 2 TB |

We will support either 3 teams with the **sdc2.c16m64** or 2 teams with the **sdc2.c32m128** flavor.

# Storage configuration

The storage on the virtual machine has been configured the following way:

* There is a 2TB scratch area in: /mnt/scratch/sdc2
* The SDC2 datacube is available in: /mnt/sdc2-datacube/sky_full.fits (read-only)
