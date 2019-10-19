

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
