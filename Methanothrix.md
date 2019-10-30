#


#
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Genome_annotations_Methanogens/Methanothrix

grep 'Nov_Mud_rebin_metabat\.27' /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Genome_annotations_Methanogens/DRAM_MGdb89_25k_annotations/annotations.tsv > Nov_Mud_rebin_metabat.27.tsv

grep -f Hydrogenase_KO.txt Nov_Mud_rebin_metabat.27.tsv >Hydrogenase_Nov_Mud_rebin_metabat.27.txt

grep 'permease' Nov_Mud_rebin_metabat.27.tsv >Permease_Nov_Mud_rebin_metabat.27.txt
grep 'transporter' Nov_Mud_rebin_metabat.27.tsv >Transporter_Nov_Mud_rebin_metabat.27.txt
