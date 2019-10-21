## Loki_asgard MAGs from OWC genomes annotations

#MAGs from d__Archaea;p__Asgardarchaeota;c__Lokiarchaeia;o__;f__;g__;s__ in OWC
```
#summit
O3C3D4_DDIG_metabat.474.fa; with mcr

#d__Archaea;p__Asgardarchaeota;c__Lokiarchaeia;o__;f__;g__;s__
O3D3D3_DDIG_megahit.356
O3C3D4_DDIG_metabat.474
OWC_substrative_co_megahit_Deep_metabat.666
O3C3D3_DDIG_MN.671
O3C3D4_DDIG_MN.839

```

#hmm profiles
```
mcrA_C_PF02249.hmm
mcrA_N_PF02745.hmm

PF02745, PF02249, 
#TIGRfam
http://genome-properties.jcvi.org/cgi-bin/GenomePropDefinition.cgi?prop_acc=GenProp0719

Step Name	Step Num	Required	Evidence (Method)	Evidence Go Terms
methyl-coenzyme M reductase, alpha subunit	alpha	YES	TIGR03256 (HMM): methyl-coenzyme M reductase, alpha subunit	
methyl-coenzyme M reductase, beta subunit	beta	YES	TIGR03257 (HMM): methyl-coenzyme M reductase, beta subunit	
methyl-coenzyme M reductase, gamma subunit	gamma	YES	TIGR03259 (HMM): methyl-coenzyme M reductase, gamma subunit	
methyl coenzyme M reductase system, component A2	mcr_A2	YES	TIGR03269 (HMM): methyl coenzyme M reductase system, component A2	
methyl-coenzyme M reductase I operon protein C	oper_C	YES	TIGR03264 (HMM): methyl-coenzyme M reductase I operon protein C	
methyl-coenzyme M reductase operon protein D	oper_D	YES	TIGR03260 (HMM): methyl-coenzyme M reductase operon protein D
```

#Annotree search of hmm in Asgard
```
no mcr in Asgard
```

#mapping of metaG to Loki with mcr, for Anvio and refineM
#check https://github.com/liupfskygre/anvio_OWC_notes_liupf/blob/master/anvio_refine_dRep_Methanogens.md.md

```
#summit
O3C3D4_DDIG_metabat.474.fa; with mcr

#cd /scratch/summit/liupf@colostate.edu/Methangoens_db_Cp50Ctl25_Anvio/

sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_DDIG_metabat.474 O3C3D4_DDIG_metabat.474.fa 

#d__Archaea;p__Asgardarchaeota;c__Lokiarchaeia;o__;f__;g__;s__

#zenith
mkdir Asgardarchaeota_Lokiarchaeia

cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Asgardarchaeota_Lokiarchaeia
# copy these genomes into this folder

O3D3D3_DDIG_megahit.356 #deRep one
O3C3D4_DDIG_MN.839 #deRep one, should be the same as 474 
O3C3D3_DDIG_MN.671

sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3D3D3_DDIG_megahit.356 O3D3D3_DDIG_megahit.356.fa
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D4_DDIG_MN.839 O3C3D4_DDIG_MN.839.fa
sbatch run_bbmap_summit_MetaG16_Mg24_2.sh metaG16_raw_reads.txt O3C3D3_DDIG_MN.671 O3C3D3_DDIG_MN.671.fa

#transfer to zenith

#sort sam file
for file in *.sam
do
echo "${file%.*}"
samtools view -@ 6 -bS $file > "${file%.*}".bam
samtools sort -@ 6 "${file%.*}".bam > "${file%.*}".sorted.bam
rm $file
rm "${file%.*}".bam
done

#transfer data to Mac and use Anvio

## 839
ls -1 *.bam > sorted_bam.txt
for sample in $(cat sorted_bam.txt)
do 
anvi-init-bam $sample -o "${sample%.*}"_index.bam
done

#creat
anvi-gen-contigs-database -f O3C3D4_DDIG_MN.839.fa -n 'Loki_anvio'
anvi-run-hmms -c contigs.db

#profile
for bam in *sorted_index.bam
do 
anvi-profile -c contigs.db -i $bam  -o ./"${bam%.*}" -T 2 
done
#
anvi-merge */PROFILE.db -o Loki_merged_profile -c contigs.db --sample-name Loki_merged_profile

#collection from outside
grep '>' O3C3D4_DDIG_MN.839.fa > seq_header.txt
sed -i -e 's/>//g' seq_header.txt
sed -i -e 's/$/\tMAGs_from_megahit/g' seq_header.txt

#import collections
anvi-import-collection -C Meta_collection -p Loki_merged_profile/PROFILE.db -c contigs.db seq_header.txt --contigs-mode

#summary
anvi-summarize -p Loki_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o Before_Refine_summary

#anvio refine
anvi-refine -p Loki_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -b MAGs_from_megahit
anvi-summarize -p Loki_merged_profile/PROFILE.db -c contigs.db -C Meta_collection -o After_refined_summary 

```

#refineM on Asgard
```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Asgardarchaeota_Lokiarchaeia

#
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Asgardarchaeota_Lokiarchaeia/O3C3D4_DDIG_MN.839_bbmap_out
for file in O3C3D4_DDIG_MN.839_OWC_*.bam
do
samtools index $file
done

refinem scaffold_stats -c 2 -x fa  O3C3D4_DDIG_MN.839.fa ./ O3C3D4_DDIG_MN.839_stats_output O3C3D4_DDIG_MN.839_OWC_*.bam

refinem outliers ./O3C3D4_DDIG_MN.839_stats_output/scaffold_stats.tsv O3C3D4_DDIG_MN.839_outlier_output_no_cov

##in addition, use the cov_correlation, 0.6
refinem outliers ./O3C3D4_DDIG_MN.839_stats_output/scaffold_stats.tsv O3C3D4_DDIG_MN.839_outlier_output_cov6 --cov_corr 0.6

#output more than 400 outliers, but the contamination value of CheckM is as low as 1.5%?
# very hard to confirm the real contaminations?

```

#DFAST
#done
```


```


#eggnog
#done
```
/Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Genome_annotations_Methanogens/Lokiarchaeia/Asgardarchaeota_Lokiarchaeia_MAGs 

prodigal -i O3D3D3_DDIG_megahit.356.fa -p meta -a O3D3D3_DDIG_megahit.356_prodigal.faa

prodigal -i O3C3D3_DDIG_MN.671.fa -p meta -a O3C3D3_DDIG_MN.671_prodigal.fa
prodigal -i O3C3D4_DDIG_MN.839.fa -p meta -a O3C3D4_DDIG_MN.839_prodigal.fa
prodigal -i O3C3D4_DDIG_metabat.474.fa -p meta -a O3C3D4_DDIG_metabat.474_prodigal.fa


```


#
#Blast to search link contigs in metagenomes??
```

```
