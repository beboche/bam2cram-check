
# bam2cram-check

This package is for checking that the file format convertion between a BAM and a CRAM leaves the data unaffected. The checks rely on the comparison between samtools stats' (CHK field), and on samtools flagstat. In addition to this both files are samtools quickcheck-ed. The stats are generated for both files. However, if there is a .stats or .flagstat file in the directory where each file is, then it will use those.

For running this you need:
```
python >= 3.5
samtools >=1.3
```

Usage:
```bash
python main.py -b <bam_file> -c <cram_file> -e <err_file> --log <log_file> -s -r <ref_file>
```
New features:
-r R        File path to the genome reference fasta file
-s          run in slurm environnment (generates srun -N1 -c1 commands)


Or alternatively, there is also a shell script for checking a full directory of BAMs and CRAMs by submitting as a job to LSF for each pair of files converted:
```bash
./run_batch.sh <bam_dir> <cram_dir> <log_dir> <output_dir> <issues_dir>
```
where each BAM-CRAM conversion to be checked will have its own file in:
- log_dir - for the logging all the commands ran and their results
- output_dir - what is sent to stdout by the commands ran
- issues_dir - what is sent to stderr by the commands ran

There is no need to create these dirs beforehands as the shell script creates them if they don't exist already.
