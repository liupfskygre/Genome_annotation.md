##genomes of interesting from OWC, novel MAGs substrates checking

#

```
O3D3D3_DDIG_megahit.448
O3C3D3_DDIG_MN.1150
OWC_substrative_co_megahit_Deep_metabat.270
OWC_substrative_co_megahit_Deep_metabat.1028
O3C3D3_DDIG_MN_Anvio.967
O3C3D4_DDIG_metabat.474
Aug_M2_C1_D5_megahit_metabat.37
May_M1_C1_D3_megahit_metabat.45
O3C3D3_metabat_w_DDIG_2.5k.322
O3D3_metabatSS.Anvio.87

#O3D3D3_DDIG_megahit.1094; not use
O3C3D3_DDIG_MN.466


```

## annotation location
```
#all summary here
cd /home/projects/Wetlands/All_genomes/OWC_MAGs_dRep_19Sept19/OWC_MAGs_19Sept19_dRep_/relabeled_dereplicated_genomes/all_bins_combined_3217db_DISTILLED_fix

cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/modeling\ of\ methanogens/genome-sub-checking

#annotation here
all_bins_combined_3217db_annotations_gtdbtk_rel95.txt

#grep -w -f all_bins_combined_3217db_annotations_gtdbtk_rel95.txt > checking12_annotations_gtdbtk_rel95_liu.txt

for file in $(cat liu_chekcing_sub.txt)
do 
grep -w "${file}" all_bins_combined_3217db_annotations_gtdbtk_rel95.txt > "${file}"_annotations_gtdbtk_rel95_liu.txt
done

for file in $(cat liu_chekcing_sub.txt)
do
cp -r /home/projects/Wetlands/All_genomes/OWC_MAGs_dRep_19Sept19/OWC_MAGs_19Sept19_dRep_/relabeled_dereplicated_genomes/relabeled_bins/DRAM_directories/"${file}"_DRAMOUT ./liu_checking_MAGs
done
```
#find 5

#others
```
cd /home/projects/Wetlands/All_genomes/OWC_MAGs_dRep_19Sept19/OWC_MAGs_19Sept19_dRep_/relabeled_dereplicated_genomes/relabeled_bins/DRAM_directories/

cp -r O3C3D3_DDIG_MN.967_DRAMOUT ../../liu_checking_MAGs/

cp -r O3C3D3_metabat_w_DDIG_2-5kb.322_DRAMOUT ../../liu_checking_MAGs/

cp -r O3C3D3_DDIG_MN.466_DRAMOUT ../../liu_checking_MAGs/

```

#for kegg mapper
```

cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/modeling\ of\ methanogens/genome-sub-checking/DRAM_OUT_tsv 

cat Aug_M2_C1_D5_megahit_metabat.37_annotations_gtdbtk_rel95_liu.txt |cut -f1,8 -d$'\t' > Aug_M2_C1_D5_megahit_metabat.37_ko.txt

cat OWC_substrative_co_megahit_Deep_metabat.1028_annotations_gtdbtk_rel95_liu.txt |cut -f1,8 -d$'\t' > OWC_substrative_co_megahit_Deep_metabat.1028_ko.txt

```

#decoder prepare
```
#log, 11 MAGs 
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/modeling of methanogens/genome-sub-checking/DRAM_OUT_tsv

#with previous DB89 annotation
DB-89-annotations.tsv > 

O3C3D3_DDIG_MN_Anvio.967 
O3C3D4_DDIG_metabat.474
May_M1_C1_D3_megahit_metabat.45
O3D3_metabatSS.Anvio.87


for file in $(cat ../MAGs_in_DB89_annotation.txt)
do
grep -w "${file}" ../DB-89-annotations.tsv >"${file}"_DRAM_annotation.txt
done

#Done
O3C3D3_metabat_w_DDIG_2.5k.322

#

cat *_liu.txt > Genome_DRAM_grdbtk_rel95_subChecking.txt
awk -F '\t' '$8!=""' Genome_DRAM_grdbtk_rel95_subChecking.txt  >Genome_DRAM_grdbtk_rel95_subChecking_w_KO.txt
cat Genome_DRAM_grdbtk_rel95_subChecking_w_KO.txt|cut -f2,8 -d$'\t' >Genome_DRAM_grdbtk_rel95_subChecking_w_KO28.txt


cat *DRAM_annotation.txt > Genome_DRAM_grdbtk_DB89_subChecking.txt

awk -F '\t' '$9!=""' Genome_DRAM_grdbtk_DB89_subChecking.txt  >Genome_DRAM_grdbtk_DB89_subChecking_w_KO.txt
cat Genome_DRAM_grdbtk_DB89_subChecking_w_KO.txt|cut -f2,9 -d$'\t' >Genome_DRAM_grdbtk_DB89_subChecking_w_KO29.txt

cat Genome_DRAM_grdbtk_rel95_subChecking_w_KO28.txt Genome_DRAM_grdbtk_DB89_subChecking_w_KO29.txt > Genome_DRAM_subChecking_w_KO.txt



sed -i -e 's/\,/\t/g' Genome_DRAM_subChecking_w_KO.txt
awk -F '\t' 'BEGIN{ORS=RS="\n"} {for(a=2; a<=NF;) print $1"\t"$(a++)}' Genome_DRAM_subChecking_w_KO.txt>Genome_DRAM_subChecking_w_KO_fix.txt

#sed -i -e 1b -e '/fasta/d' Desulfobacterota_BSN033_annotation_w_KO28_fix.tsv
sed -i -e '/fasta/d' Genome_DRAM_subChecking_w_KO_fix.txt

sed -i -e 's/_/;/g' Genome_DRAM_subChecking_w_KO_fix.txt

awk '{print $1"_"NR"\t"$2}' Genome_DRAM_subChecking_w_KO_fix.txt > Genome_DRAM_subChecking_w_KO_fix_wNR.txt

conda activate Decoder
KEGG-decoder --input Genome_DRAM_subChecking_w_KO_fix_wNR.txt --output Checking11_FUNCTION_OUT.list --vizoption interactive

```

#kegg mapper
```
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/modeling\ of\ methanogens/genome-sub-checking/DRAM_OUT_tsv/KEGG_Decoder

cat May_M1_C1_D3_megahit_metabat.45_DRAM_annotation.txt|cut -f1,9 -d$'\t' > May_M1_C1_D3_megahit_metabat.45_DRAM_annotation_ko28.txt

cat O3C3D3_DDIG_MN_Anvio.967_DRAM_annotation.txt|cut -f1,9 -d$'\t' > O3C3D3_DDIG_MN_Anvio.967_DRAM_annotation_ko28.txt

cat O3D3_metabatSS.Anvio.87_DRAM_annotation.txt|cut -f1,9 -d$'\t' > O3D3_metabatSS.Anvio.87_DRAM_annotation_k28.txt

```


#adding one genomes; Aug-20-2020;==>O3C3D3_metabat_w_DDIG_2-5kb.49 

```
#checked MAGs with new annotation are tem put here
/home/projects/Wetlands/All_genomes/OWC_MAGs_dRep_19Sept19/OWC_MAGs_19Sept19_dRep_/relabeled_dereplicated_genomes/liu_checking_MAGs

#on MAC 
cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/modeling\ of\ methanogens/genome-sub-checking/DRAM_OUT_tsv/KEGG_Decoder

#1, first adding to keggdocer file and rerun all genomes
awk -F '\t' '$8!=""' O3C3D3_metabat_w_DDIG_2-5kb.49_annotations_r95.tsv >O3C3D3_metabat_w_DDIG_2-5kb.49_annotations_r95_wKO.tsv

cat O3C3D3_metabat_w_DDIG_2-5kb.49_annotations_r95_wKO.tsv|cut -f2,8 -d$'\t' >O3C3D3_metabat_w_DDIG_2-5kb.49_annotations_r95_k028.tsv

O3C3D3_metabat_w_DDIG_2-5kb.49_annotations_r95.tsv
#2, go through the excel annotation file and pick evidences for this one

cat O3C3D3_metabat_w_DDIG_2-5kb.49_annotations_r95_k028.tsv Genome_DRAM_grdbtk_rel95_subChecking_w_KO28.txt Genome_DRAM_grdbtk_DB89_subChecking_w_KO29.txt > Genome_DRAM_subChecking_w_KO.txt



sed -i -e 's/\,/\t/g' Genome_DRAM_subChecking_w_KO.txt
awk -F '\t' 'BEGIN{ORS=RS="\n"} {for(a=2; a<=NF;) print $1"\t"$(a++)}' Genome_DRAM_subChecking_w_KO.txt>Genome_DRAM_subChecking_w_KO_fix.txt

sed -i -e '/fasta/d' Genome_DRAM_subChecking_w_KO_fix.txt

sed -i -e 's/_/;/g' Genome_DRAM_subChecking_w_KO_fix.txt

awk '{print $1"_"NR"\t"$2}' Genome_DRAM_subChecking_w_KO_fix.txt > Genome_DRAM_subChecking_w_KO_fix_wNR.txt

conda activate Decoder
KEGG-decoder --input Genome_DRAM_subChecking_w_KO_fix_wNR.txt --output Checking12_FUNCTION_OUT.list --vizoption interactive

```
