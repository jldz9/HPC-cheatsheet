You can copy the batch script below to use `sbatch run.sh` to submit 

## CSU
### Cashew

!!! Note
    remove `#SBATCH --gres=gpu:1 ` if you do not want to use GPU

```bash
#!/bin/bash

#SBATCH --job-name=dev 
#SBATCH --output=codetunnel_%j.out
#SBATCH --error=codetunnel_%j.err
#SBATCH --time=1-00:00:00
#SBTACH --partition=all
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=32
#SBATCH --gres=gpu:1 
#SBATCH --mem=64G
#SBATCH --nodes=1
#SBATCH --mail-user=youremail@colostate.edu
#SBATCH --mail-type=ALL

echo "Job started"

##put your command here##

wait

echo "Job finished"

```

### Riviera

!!! Note
    remove `#SBATCH --gres=gpu:1 ` if you do not want to use GPU

```bash
#!/bin/bash

#SBATCH --job-name=dev 
#SBATCH --output=codetunnel_%j.out
#SBATCH --error=codetunnel_%j.err
#SBATCH --time=1-00:00:00
#SBTACH --partition=day-long-gpu
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=32
#SBATCH --gres=gpu:1 
#SBATCH --mem=64G
#SBATCH --nodes=1
#SBATCH --mail-user=youremail@colostate.edu
#SBATCH --mail-type=ALL

echo "Job started"

##put your command here##

wait

echo "Job finished"

```