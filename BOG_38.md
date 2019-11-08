#BOG_38.md

#

#download 50 genomes from NCBI
```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/BOG_38_assemblies

#wget ftp://ftp.ncbi.nlm.nih.gov/genomes/refseq/archaea/assembly_summary.txt 
# download ftp address
wget ftp://ftp.ncbi.nlm.nih.gov/genomes/genbank/archaea/assembly_summary.txt 

#
nano BOG_38_MAGs50.list
sed -i -e 's/\.1$//1' BOG_38_MAGs50.list
#get BOG ftp download list
grep -f BOG_38_MAGs50.list assembly_summary.txt  > BOG_38_MAGs50_assembly_summary.txt

#get ftp add for BOG-38, 50 genomes
awk -F '\t' '{print $20}' BOG_38_MAGs50_assembly_summary.txt> BOG_38_MAGs50_assembly_summary_ftp.txt

#get genomes.fna, 50

for next in $(cat BOG_38_MAGs50_assembly_summary_ftp.txt);
do wget --timestamping -P ./  "$next"/*genomic.fna.gz; # 
done

#de compress, keep orignal file with -k 
# gunzip -k *.gz
gunzip *.gz
```
