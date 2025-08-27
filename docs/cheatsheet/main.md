This page will list cheat sheet for different HPC groups, you may use catalogs to find specific HPC

## SciNet
### Ceres

***Login***

| Method | Code/Link | Note |
| ------| ----- | -----|
| Login | `ssh user.name@ceres.scinet.usda.gov` | Replace the `user.name` with your username in Scinet |
| DTN Login | `ssh user.name@ceres-dtn.scinet.usda.gov` | DTN refer to data transfer node |
| GUI | [Open Ondemand](http://ceres-ood.scinet.usda.gov/) | [Login tutorial](https://scinet.usda.gov/guides/access/login#accessing-gui-based-services) and [Usage](https://scinet.usda.gov/guides/software/open-ondemand)|


***Data Transfer***
!!! note
    Example to copy a directory from your local system to the HPC 

    Simply switch the order if you want transfer HPC --> local


| Method | Code/Link | Note |
| ------| ----- | -----|
| Windows | `scp -r path\to\target  user.name@ceres-dtn.scinet.usda.gov:/path/to/dest` |  use " \ " on for windows path seperator, also if you are copying files instead of directory, remove `-r` |
| Linux | `rsync -avz --no-p --no-g /path/to/target <user.name>@ceres-dtn.scinet.usda.gov:/path/to/dest` | |
| MacOS | `rsync -avz --no-p --no-g /path/to/target <user.name>@ceres-dtn.scinet.usda.gov:/path/to/dest` | Use `--iconv utf-8-mac` if run into issue [source](https://odd.blog/2020/10/06/rsync-between-mac-and-linux/) |
| GUI | [Globus](https://www.globus.org/) | [Instruction](https://scinet.usda.gov/guides/data/datatransfer#globus-data-transfer)|

***Compute*** 
!!! warning
    Do not run computational intensive job on login node, you need to allocate a computing node

| Method | Code/Link | Note |
| ------| ----- | -----|
| Allocate resource | `salloc -n 2 -N 1 --mem 128G --cpus-per-task 8 -p short -t 01:00:00` | Reserve `-n 2` tasks  in `-N 1` Node  with `--mem=128GB` memory under `-p short` partitions  for `-t 1` hour, Ceres gives you an interactive shell after allocated the resource |
| Job run | `srun salloc -n 8 -N 1 --mem=128G -p=short -t 01:00:00 your_command` | Similiar with `salloc` but you can run your command use `srun` and specific the resource you need | 
| Batch run | [Batch script generator](https://scinet.usda.gov/support/ceres-job-script) | Generally like to combine multiple `srun` together , check [Tutorial](https://scinet.usda.gov/guides/use/slurm#batch-mode) for more detail|
| Check job | `squeue -A` | |
| Cancel job | `scancel jobID`| JobID can be obtained from `squeue` |

***Software*** 


| Method | Code/Link | Note |
| ------| ----- | -----|
| Check module availibility | `module avail your_module` | your_module refer to the actual module name | 
| load module | `module load your_module` | If there are different versions for your_module, this will load the default version, use your_module/version_number to load the version you want  |
| self install software | `module load miniconda; conda install or pip install` | This will load Conda package manager and allow you to self-install package, check [Toturial](https://scinet.usda.gov/guides/software/conda)|
| Use container | `module load apptainer; apptainer foo` | HPC environment cannot allow docker because of user privilege, [apptainer](https://apptainer.org/) is a great alternative | 


### Atlas


***Access***

| Method | Code/Link | Note |
| ------| ----- | -----|
| Login | `ssh user.name@Atlas-login.hpc.msstate.edu` | Replace the `user.name` with your username in Scinet |
| DTN Login | `ssh user.name@Atlas-dtn.hpc.msstate.edu` | DTN refer to data transfer node |
| GUI | [Open Ondemand](https://atlas-ood.hpc.msstate.edu/) | [login tutorial](https://scinet.usda.gov/guides/access/login#accessing-gui-based-services) and [Usage](https://www.hpc.msstate.edu/computing/atlas/ood.php)|

***Data Transfer***
!!! note
    Example to copy a directory from your local system to the HPC 

    Simply switch the order if you want transfer HPC --> local


| Method | Code/Link | Note |
| ------| ----- | -----|
| Windows | `scp -r path\to\target  user.name@Atlas-dtn.hpc.msstate.edu:/path/to/dest` |  use " \ " on windows path, also if you are copying files instead of directory, remove `-r`|
| Linux | `rsync -avz --no-p --no-g /path/to/target <user.name>@Atlas-dtn.hpc.msstate.edu:/path/to/dest` | |
| MacOS | `rsync -avz --no-p --no-g /path/to/target <user.name>@Atlas-dtn.hpc.msstate.edu:/path/to/dest` | Use `--iconv utf-8-mac` if run into issue [source](https://odd.blog/2020/10/06/rsync-between-mac-and-linux/) |
| GUI | [Globus](https://www.globus.org/) | [Instruction](https://scinet.usda.gov/guides/data/datatransfer#globus-data-transfer)|


***Compute*** 
!!! warning
    Do not run computational intensive job on login node, you need to allocate a computing node

| Method | Code/Link | Note |
| ------| ----- | -----|
| Allocate resource | `salloc -n 2 -N 1 --cpus-per-task 8 --mem 128G -p short -t 01:00:00 -A your_user_group` | Atlas does not excute interactive shell after use `salloc` and requires user group input, the user group typically is your project name, check Miscellaneous section in the cheat sheet for how to get your user group |
| Interactive | `srun salloc -n 1 -N 1 --mem=128G -p=short -t 01:00:00 -A your_user_group --pty bash` | Get a shell on a compute job | 
| job run | `srun salloc -n 1 -N 1 --mem=128G -p=short -t 01:00:00 -A your_user_group your_command` | Similiar with `salloc` but you can run your command use `srun` and specific the resource you need |
| Batch run | [Batch script generator](https://www.hpc.msstate.edu/computing/atlas/#Atlas%20Job%20Script%20Generator:~:text=Atlas%20Job%20Script%20Generator)| Generally like to combine multiple `srun` together , check [Tutorial](https://www.hpc.msstate.edu/computing/atlas/#Atlas%20Job%20Script%20Generator:~:text=SBATCH%20Submits%20a%20job%20runscript%20for%20later%20execution%20(batch%20mode)) for more detail|
| Check job | `squeue -A "Your user group"` | |
| Cancel job | `scancel jobID`| JobID can be obtained from `squeue` |


***Software*** 

| Method | Code/Link | Note |
| ------| ----- | -----|
| Check module availibility | `module avail your_module` | your_module refer to the actual module name | 
| load module | `module load your_module` | If there are different versions for your_module, this will load the default version, use your_module/version_number to load the version you want  |
| self install software | `module load miniconda; conda install or pip install` | This will load Conda package manager and allow you to self-install package, check [Toturial](https://scinet.usda.gov/guides/software/conda)|
| Use container | `module load apptainer; apptainer foo` | HPC environment cannot allow docker because of user privilege, [apptainer](https://apptainer.org/) is a great alternative | 


## CSU

### [Cashew](https://www.engr.colostate.edu/ets/cashew-cluster/)

***Login***

| Method | Code/Link | Note |
| ------| ----- | -----|
| Login | `ssh user.name@cashew.engr.colostate.edu` | Replace the `user.name` with your username in Scinet |
| GUI | [Open Ondemand](https://cashew-ondemand.engr.colostate.edu/pun/sys/dashboard) | |

***Data Transfer***

!!! note
    Example to copy a directory from your local system to the HPC 

    Simply switch the order if you want transfer HPC --> local


| Method | Code/Link | Note |
| ------| ----- | -----|
| Windows | `scp -r path\to\source  user.name@cashew.engr.colostate.edu:/path/to/dest` | Use " \ " on windows path, also if you are copying files instead of directory, remove `-r` |
| Linux | `rsync -avz --no-p --no-g /path/to/source user.name@cashew.engr.colostate.edu:/path/to/dest` | |
| MacOS | `rsync -avz --no-p --no-g /path/to/source user.name@cashew.engr.colostate.edu:/path/to/dest` | Use `--iconv utf-8-mac` if run into issue [source](https://odd.blog/2020/10/06/rsync-between-mac-and-linux/) |
| GUI | [open Ondemand](https://cashew-ondemand.engr.colostate.edu/pun/sys/dashboard/) | Under Files |


***Compute*** 

!!! warning
    
    Do not run computational intensive job on login node, you need to allocate a computing node

| Method | Code/Link | Note |
| ------| ----- | -----|
| Check HPC | `sinfo` | You may find availiable partition name, time limit to be useful |
| Interactive node| `srun -n 1 -N 1 --mem 32GB --cpus-per-task 16 --gres=gpu:1 -p all -t 01:00:00 --pty bash` | Get an instance on compute node, `-n 1` task `-N 1` node `--mem 32GB` memory `--cpus-per-task 16` cpus `-gres=gpu:1` gpus `-p all` partition `-t 01:00:00` hour `--pty bash` bash shell | 
| job run | `srun -n 1 -N 1 --mem 32GB --cpus-per-task 16 --gres=gpu:1 -p all -t 01:00:00 your_job_executable` | Job will be terminated when you close the terminal, if you want background processing use `sbatch` instead |
| Batch run | [Copy Batch Script](../batch_script#cashew) | use `sbatch your_batch_file` to submit batch jobs. More detail on [cashew](https://www.engr.colostate.edu/ets/writing-a-submission-script) website |
| Check job | `squeue -u your_user_name` | or just use `squeue` to check all running instances|
| Cancel job | `scancel jobID`| JobID can be obtained from `squeue` |


***Software*** 

| Method | Code/Link | Note |
| ------| ----- | -----|
| Check module availibility | `module avail your_module` | e.g. `module avail git` | 
| load module | `module load your_module` | To load specific version, e.g. `module load git/2.46.0`  |
| self install software | `conda install` or `pip install` | Cashew will load conda and pip by default, you don't need to `module load conda`|
| Use container | Container env is not availiable on Cashew HPC |  | 


### [Riviera](https://riviera-docs.readthedocs.io/en/latest/index.html)

***Login***

| Method | Code/Link | Note |
| ------| ----- | -----|
| Login | `ssh user.name@riviera.colostate.edu` | Replace the `user.name` with your username in Scinet |
| GUI | Riviera does not support OpenOnDemand | |

***Data Transfer***

!!! note
    Example to copy a directory from your local system to the HPC 

    Simply switch the order if you want transfer HPC --> local


| Method | Code/Link | Note |
| ------| ----- | -----|
| Windows | `scp -r path\to\source  user.name@cashew.engr.colostate.edu:/path/to/dest` | Use " \ " on windows path, if you are copying files instead of directory, remove `-r` |
| Linux | `rsync -avz --no-p --no-g /path/to/source user.name@cashew.engr.colostate.edu:/path/to/dest` | |
| MacOS | `rsync -avz --no-p --no-g /path/to/source user.name@cashew.engr.colostate.edu:/path/to/dest` | Use `--iconv utf-8-mac` if run into issue [source](https://odd.blog/2020/10/06/rsync-between-mac-and-linux/) |
| GUI | Riviera does not support web GUI for data transfer, |User could use winSCP instead |


***Compute*** 

!!! warning
    
    Do not run computational intensive job on login node, you need to allocate a computing node

!!! note
    Riviera HPC does not load slurm by default, run ```
    module load slurm ``` first to load slurm module

| Method | Code/Link | Note |
| ------| ----- | -----|
| Check HPC | `sinfo` | You may find availiable **partition** name, **time limit** to be useful |
| Interactive node| `srun -n 1 -N 1 --mem 32GB --cpus-per-task 16 --gres=gpu:1 -p day-long-gpu -t 01:00:00 --pty bash` | Get an instance on compute node, `-n 1` task `-N 1` node `--mem 32GB` memory `--cpus-per-task 16` cpus `-gres=gpu:1` gpus `-p day-long-gpu` partition `-t 01:00:00` hour `--pty bash` bash shell | 
| job run | `srun -n 1 -N 1 --mem 32GB --cpus-per-task 16 --gres=gpu:1 -p day-long-gpu -t 01:00:00 your_job_executable` | Job will be terminated when you close the terminal, if you want background processing use `sbatch` instead |
| Batch run | [Copy Batch Script](../batch_script#riviera) | use `sbatch your_batch_file` to submit batch jobs. More detail on [cashew](https://www.engr.colostate.edu/ets/writing-a-submission-script) website |
| Check job | `squeue -u your_user_name` | or just use `squeue` to check all running instances|
| Cancel job | `scancel jobID`| JobID can be obtained from `squeue` |

***Software*** 

| Method | Code/Link | Note |
| ------| ----- | -----|
| Check module availibility | `module avail your_module` | e.g. `module avail git` | 
| load module | `module load your_module` | To load specific version, e.g. `module load git/2.46.0`  |
| self install software | `conda install` or `pip install` | Riviera will load conda and pip by default, you don't need to `module load conda`|
| Use container | `module load singularity` | Only Singularity availiable, apptainer is not supported | 

