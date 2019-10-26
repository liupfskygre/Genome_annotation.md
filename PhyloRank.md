

https://github.com/dparks1134/PhyloRank

#installation on mac in a virtual environment
```
#try python 3.7
conda create -n Phylorank_py3 python=3.7
conda activate Phylorank_py3
conda remove --name Phylorank_py3  --all

#should be python 2.7
conda create -n Phylorank_py27 python=2.7
conda activate Phylorank_py27
conda deactivate
conda install -n Phylorank_py27 numpy matplotlib mpld3 jinja2 dendropy
conda install -n Phylorank_py27 scipy
```

```
phylorank -h

                ...::: PhyloRank v0.0.39 :::...

  Curation methods:
    outliers    -> Create RED table, scaled tree, and plot useful for identifying taxonomic outliers
    compare_red -> Compare RED values of taxa calculated over different trees
    rd_ranks    -> Calculate number of taxa for specified RED thresholds
    dist_plot   -> Plot distribution of taxa in each taxonomic rank
    mark_tree   -> Mark nodes with distribution information and predicted taxonomic ranks
    rogue_test  -> Index indicating the incongruence of genomes over a set of tree

  Taxonomy decoration and inspection methods:
    decorate    -> Place internal taxonomic labels on tree
    taxon_stats -> Summary statistics of taxonomic groups
    rank_res    -> Calculate taxonomic resolution at each rank
    
  Mean branch length to extant taxa methods:
    bl_dist     -> Calculate distribution of branch lengths at each taxonomic rank
    bl_optimal  -> Determine branch length for best congruency with existing taxonomy
    bl_decorate -> Decorate tree using a mean branch length criterion
    bl_table    -> Produce table with number of lineage for increasing mean branch lengths
  
  [Expert commands: hide these at some point]

  robustness_plot -> Plot relative distance of groups across a set of trees.


  Use: phylorank <command> -h for command specific help.
```


#
```

cd /Users/pengfeiliu/A_Wrighton_lab/Wetland_project/OWC_metaG_2014_2018/OWC_wetland_methanogens_database/Methanogens_final_dRep_clean_db/Methanogens_cleanDB89_OCt3_tree

conda activate Phylorank_py27

gtdbtk.ar122.rooted.tree

phylorank decorate input_tree taxonomy_file output_tree
gtdbtk.ar122.rooted.tree

# get taxonomy file
grep '>' gtdbtk.ar122.msa.fasta > taxonomy_file_ref.txt
sed -i -e 's/>//1' taxonomy_file_ref.txt
sed -i -e 's/ /\t/1' taxonomy_file_ref.txt
grep 'd__' taxonomy_file_ref.txt >taxonomy_file_ref_gtdb_AR.txt

#add tax of MAGs to the file

$ phylorank decorate --skip_rd_refine gtdbtk.ar122.rooted.tree taxonomy_file_ref_gtdb_AR.txt MGdb89_gtdbtk_r89.ar122.rooted.decorated.tree
#done, interpretation??


phylorank outliers MGdb89_gtdbtk_r89.ar122.rooted.decorated.tree taxonomy_file_ref_gtdb_AR.txt MGdb89_gtdbtk_r89.rooted_outliers_out

```


```
phylorank dist_plot gtdbtk.ar122.rooted.tree gtdbtk.ar122.rooted.tree_dist_pot

```
