# 

#OWC_substrative_co_megahit_Deep_metabat.1028
```
#cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Methanogens_final_dRep_clean_db/DRAM_MGdb89_25k_annotations

grep 'OWC_substrative_co_megahit_Deep_metabat\.1028' annotations.tsv > OWC_substrative_co_megahit_Deep_metabat.1028.annotations.tsv

```

#eggnog, mapper v2
```
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Genome_annotations_Methanogens/Methanomassiliicoccales
prodigal -i OWC_substrative_co_megahit_Deep_metabat.1028.fa -p meta -a OWC_substrative_co_megahit_Deep_metabat.1028_prodigal.faa
```
