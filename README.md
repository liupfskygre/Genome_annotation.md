# Genome_annotation.md

#Genome annotation highlight references
```
1. Seitz, K. W. et al. Asgard archaea capable of anaerobic hydrocarbon cycling. Nat. Commun. 10, (2019).
#database based and homology search based genome annotation, inludes many mannual database curation and verifcation, methods well described

```




May use DRAM et al. tools to annotate genomes or MAGs


1. use DRAM to do annotation, check annotation with KO
2. mapping KO in KEGG mapper (https://www.genome.jp/kegg/mapper.html), reconstruct pathway
3. check genes without KO, fill pathway gaps
4. verify the gene predictions based gene cluster, operon, and further homolog search (blast/hmmsearch)
5. build subsystem/module style SOM excel table for further checking (methanogensis et al.)
6, verify using eggnog and draft (both have similar annotation results)





#specific targeted annotations

#based on metaT and completeness%
Methanothrix Genomes from Jordan’s dissertation is no published yet

#pick representatives for each cluster of methanogens based on Cp%-Ct% and mcrA
#position in the tree (novel groups first)

Most active methanogens based on Max-metaT
Methanothrix sp002256595 clusters TPM;

s__Methanothrix sp002256595
Nov_Mud_rebin_metabat.27


f__Methanoregulaceae
#Aug_M1_C1_D3_megahit_metabat_Anvio.266 
O3C3D3_metabat_w_DDIG_2.5k.67

o__Methanomicrobiales, OWC cluster 
O3C3D3_metabat_w_DDIG_2.5k.225 (w/ mcrA) but not active

f__ Methanocullaceae
MUD_2014_2015_coassembly_Metabat_69

f__Methanoperedenaceae
O3C3D3_DDIG_MN.971

o__Methanomassiliicoccales
OWC_substrative_co_megahit_Deep_metabat.1028

d__Archaea;p__Halobacterota;c__Methanomicrobia;o__Methanomicrobiales;f__Methanospirillaceae;g__Methanospirillum;s__
O3D3D3_DDIG_megahit.259
