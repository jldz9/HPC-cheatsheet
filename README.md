# Scinet Cheatsheet
SCINet is the USDA-ARS’s initiative for scientific computing.

The high-performance computing (HPC) resources of Scinet currently include ***Ceres*** and ***Altas***

This tutorial is meant to let user quick start on HPC, for detailed instruction please refer to [Ceres](https://scinet.usda.gov/guides/start) and [Atlas](https://www.hpc.msstate.edu/computing/atlas/)

This tutorial also assume you have access to Scinet and alreay initilized the login credentials, if not, check [Tutorial](https://scinet.usda.gov/guides/access/login)

 ### Ceres
--------------------

***Access***
| Method | Code/Link | Note |
| ------| ----- | -----|
| Login | `ssh user.name@ceres.scinet.usda.gov` | |
| DTN Login | `ssh user.name@ceres-dtn.scinet.usda.gov` | DTN refer to data transfer node |
| GUI | [Open Ondemand](http://ceres-ood.scinet.usda.gov/) | [login tutorial](https://scinet.usda.gov/guides/access/login#accessing-gui-based-services) and [Usage](https://scinet.usda.gov/guides/software/open-ondemand)|<br />
<br />

***Data Transfer***
| Method | Code/Link | Note |
| ------| ----- | -----|
| Windows | `scp -r path\to\target  user.name@ceres-dtn.scinet.usda.gov:/path/to/dest` | Tested on Windows 11 powershell, use " \ " on windows path since windows like it better |
| Linux | `rsync -avz --no-p --no-g /path/to/target <user.name>@ceres-dtn.scinet.usda.gov:/path/to/dest` | |
| MacOS | `rsync -avz --no-p --no-g /path/to/target <user.name>@ceres-dtn.scinet.usda.gov:/path/to/dest` | Use `--iconv utf-8-mac` if run into issue [source](https://odd.blog/2020/10/06/rsync-between-mac-and-linux/) |
| GUI | [Globus](https://www.globus.org/) | [Instruction](https://scinet.usda.gov/guides/data/datatransfer#globus-data-transfer)|<br />
<br />

***Compute*** <br />
Do not run computational intensive job on login node, you need to allocate a computing node
| Method | Code/Link | Note |
| ------| ----- | -----|
| Allocate resource | `salloc -n 8 -N 1 --mem=128G -p=short -t 01:00:00` | This means I want to reserve 8 core `-n` in 1 Node `-N` with 128GB memory `--mem` under short partitions `-p` for 1 hour `-t` |
| Job run | `srun salloc -n 8 -N 1 --mem=128G -p=short -t 01:00:00 your_command` | Similiar with `salloc` but you can run your command use `srun` and specific the resource you need | 
| Batch run | [Batch script generator](https://scinet.usda.gov/support/ceres-job-script) | Generally like to combine multiple `srun` together , check [Tutorial](https://scinet.usda.gov/guides/use/slurm#batch-mode) for more detail|
| Check job | `squeue` | |
| Cancel job | `scancel jobID`| JobID can be obtained from `squeue` |
<br />

***Software*** <br />
Software on HPC can be load as module 
| Method | Code/Link | Note |
| ------| ----- | -----|
| Check module availibility | `module avail your_module` | your_module refer to the actual module name | 
| load module | `module load your_module` | If there are different versions for your_module, this will load the default version, use your_module/version_number to load the version you want  |
| self install software | `module load miniconda; conda install or pip install` | This will load Conda package manager and allow you to self-install package, check [Toturial](https://scinet.usda.gov/guides/software/conda)|
| Use container | `module load apptainer; apptainer foo` | HPC environment cannot allow docker because of user privilege, [apptainer](https://apptainer.org/) is a great alternative | 
<br />



