## use DRAM developed in the group to annotate MAGs

#
zenith

```
source /opt/Miniconda2/miniconda2/bin/activate DRAM

DRAM.py annotate -i scaffold_error.fa -o annotated_DRAM_error --threads 24

DRAM.py summarize_genomes -i annotated_DRAM_error/annotations.tsv -o genome_summaries_error --trna_path annotated_DRAM_error/trnas.tsv

```

#unity
```
I have DRAM.py running on Unity. I made a conda environment so you need a source command to run DRAM.py.
Put these in your pbs script to run:
source /fs/byo/wrighton-data1/opt/miniconda2/bin/activate DRAM
DRAM.py annotate -i scaffold.fa -o annotated_DRAM --threads 24 &> log.txt
DRAM.py summarize_genomes -i annotated_DRAM/annotations.tsv -o genome_summaries --trna_path annotated_DRAM/trnas.tsv
source /fs/byo/wrighton-data1/opt/miniconda2/bin/deactivate
Here is my pbs script command (you may want to go higher on mem):
qsub my_DRAM_2.pbs -l walltime=5:00:00 -M wolfeerich@gmail.com -l nodes=1:ppn=24,mem=200GB

```
