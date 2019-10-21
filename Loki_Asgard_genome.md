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

```

#refineM on Asgard
```
cd /home/projects/Wetlands/2018_sampling/Methanog_targeted_coassembly/Methanogens_final_dRep_clean_db/Asgardarchaeota_Lokiarchaeia

```

#DFAST
```


```


#eggnog
```
/Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Genome_annotations_Methanogens/Lokiarchaeia/Asgardarchaeota_Lokiarchaeia_MAGs 

prodigal -i O3D3D3_DDIG_megahit.356.fa -p meta -a O3D3D3_DDIG_megahit.356_prodigal.faa

prodigal -i O3C3D3_DDIG_MN.671.fa -p meta -a O3C3D3_DDIG_MN.671_prodigal.fa
prodigal -i O3C3D4_DDIG_MN.839.fa -p meta -a O3C3D4_DDIG_MN.839_prodigal.fa
prodigal -i O3C3D4_DDIG_metabat.474.fa -p meta -a O3C3D4_DDIG_metabat.474_prodigal.fa


```
