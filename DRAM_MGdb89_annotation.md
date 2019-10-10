## using DRAM to do annotation on the methanogens genomes

```
 DRAM is now working on Zenith and work is being done to get it ready on unity. To run DRAM the command is:
DRAM.py annotate -i '/path/to/your/bins/*.fa' -o /path/to/your/annotations --threads 40 --checkm_quality /path/to/your/quality/checkM_outdir/results.tsv --gtdb_taxonomy /path/to/your/gtdbtk/results/gtdbtk.bac120.summary.tsv
To then summarize your annotations:
DRAM.py summarize_genomes -i /path/to/your/annotations/annotations.tsv -o /path/to/your/annotations/summarized --rrna_path /path/to/your/annotations/rrnas.tsv --trna_path /path/to/your/annotations/trnas.tsv

```

**zenith**, 
```
# MGdb, 89
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Methanogens_cleanDB_26Spet2019_dRep/dereplicated_genomes

#checkM file
Methanogens_cleanDB_26Spet2019_dRep_checkm_summary.txt

#due to gtdbtk, bac and arc is separated, way to combine?
Methanogens_cleanDB_26Spet2019_dRep.ar122.summary.tsv 

screen -S DRAM_MGdb89
source /opt/Miniconda2/miniconda2/bin/activate DRAM
DRAM.py annotate -i '/home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Methanogens_cleanDB_26Spet2019_dRep/dereplicated_genomes/*.fa' -o ./DRAM_MGdb89_annotations --threads 24 --checkm_quality ./Methanogens_cleanDB_26Spet2019_dRep_checkm_summary.txt --gtdb_taxonomy ./gtdbtk_out/Methanogens_cleanDB_26Spet2019_dRep.ar122.summary.tsv &>DRAM_MGdb89.log

#done 7-OCT-2019
DRAM_MGdb89_annotations
DRAM.py summarize_genomes -i ./annotations.tsv -o ./genome_summaries --trna_path ./trnas.tsv
##
#/home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Methanogens_cleanDB_26Spet2019_dRep/dereplicated_genomes/DRAM_MGdb89_annotations/genome_summaries
(DRAM) [liupf@zenith genome_summaries]$ ls
#genome_stats.tsv  genome_summary.xlsx  heatmap.html
```

## compare the annotation with hmmsearch 
```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Methanogens_cleanDB_26Spet2019_dRep/dereplicated_genomes/DRAM_MGdb89_annotations

#mcrA, K00309, mcrB, K00401, mcrG, K00402
[liupf@zenith DRAM_MGdb89_annotations]$ grep -E 'K00399' annotations.tsv
[liupf@zenith DRAM_MGdb89_annotations]$ grep -E 'K00399|K00402|K00401' annotations.tsv |wc -l


```


#examples
```
source /opt/Miniconda2/miniconda2/bin/activate DRAM

DRAM.py annotate -i scaffold_error.fa -o annotated_DRAM_error --threads 24

DRAM.py summarize_genomes -i annotated_DRAM_error/annotations.tsv -o genome_summaries_error --trna_path annotated_DRAM_error/trnas.tsv
```
