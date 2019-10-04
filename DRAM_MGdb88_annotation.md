## using DRAM to do annotation on the methanogens genomes

```
 DRAM is now working on Zenith and work is being done to get it ready on unity. To run DRAM the command is:
DRAM.py annotate -i '/path/to/your/bins/*.fa' -o /path/to/your/annotations --threads 40 --checkm_quality /path/to/your/quality/checkM_outdir/results.tsv --gtdb_taxonomy /path/to/your/gtdbtk/results/gtdbtk.bac120.summary.tsv
To then summarize your annotations:
DRAM.py summarize_genomes -i /path/to/your/annotations/annotations.tsv -o /path/to/your/annotations/summarized --rrna_path /path/to/your/annotations/rrnas.tsv --trna_path /path/to/your/annotations/trnas.tsv

```

##
