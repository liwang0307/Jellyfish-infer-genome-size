# Change directory to job submission directory (Optional!)
cd ./jellyfish
module load Jellyfish/2.3.0-GCC-8.3.0   # load module and run jellyfish as below
cat P-capsci-67_R1.fq | jellyfish count -C -m 99 -s 1000000000 -t 8 -o pcshortreads1.jf /dev/fd/0

# Generate  a histgram file
jellyfish histo pcshortreads1.jf >pcshortreads1.histo 
# download pcshortreads1.histo and drag it into http://qb.cshl.edu/genomescope/; set k-mer=99 and read length=150.
