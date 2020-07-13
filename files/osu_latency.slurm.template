#!/bin/bash

# Slurm job options (name, compute nodes, job time)
#SBATCH --job-name=[* ENTER YOUR JOB NAME HERE *] 
#SBATCH --time=0:10:0
#SBATCH --nodes=2
#SBATCH --ntasks=2
#SBATCH --tasks-per-node=1
#SBATCH --cpus-per-task=1
#SBATCH --exclusive

# Replace [budget code] below with your budget code (e.g. t01)
#SBATCH --account=[* ENTER YOUR BUDGET CODE HERE *]
# We use the "standard" partition as we are running on CPU nodes
#SBATCH --partition=standard
# We use the "standard" QoS as our runtime is less than 4 days
#SBATCH --qos=standard

module load singularity
module load intel-mpi-19

# Change to the submission directory
cd $SLURM_SUBMIT_DIR

mpiexec singularity run [* YOUR SIF IMAGE NAME *] collective/osu_gather
