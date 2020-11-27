# Jellyfish-infer-genome-size
#!/bin/bash
#SBATCH --job-name=jellyfish		    # Job name (jellyfish)
#SBATCH --partition=batch		        # Partition name (batch, highmem_p, or gpu_p)
#SBATCH --ntasks=8			            # default using 1 CPU core on a single node, I have changed it to 8
#SBATCH --cpus-per-task=8	 	        # default 1 CPU core per task, and I have changed it to 8
#SBATCH --mem=32G			              # Memory per node (4GB); I have changed from 4 GB to 32 GB because "out of memory" error message
#SBATCH --time=1:00:00              # Time limit hrs:min:sec or days-hours:minutes:seconds
#SBATCH --export=NONE               # Do not export any user’s explicit environment variables to compute node
#SBATCH --output=./log/01.out        # Standard output log, e.g., 
#SBATCH --error=./log/01.err     	  # Standard error log, e.g., 
#SBATCH --mail-user=lw78943@uga.edu # Where to send mail
#SBATCH --mail-type=END,FAIL        # Mail events (BEGIN, END, FAIL, ALL)


cd /scratch/lw78943/jellyfish			  # Change directory to job submission directory (Optional!)
module load Jellyfish/2.3.0-GCC-8.3.0   # load module and run jellyfish as below
cat P-capsci-67_R1.fq | jellyfish count -C -m 99 -s 1000000000 -t 8 -o pcshortreads1.jf /dev/fd/0

sbatch jellyfish.sub.sh  # submit script
squeue --me              # check job status
less 01.err              # check error log
q                        # exit check
# Generate  a histgram file
jellyfish histo pcshortreads1.jf >pcshortreads1.histo 
# download pcshortreads1.histo and drag it into http://qb.cshl.edu/genomescope/; set k-mer=99 and read length=150.
