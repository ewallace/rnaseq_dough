# notes.md

Progress updates on the analysis.

# 2023-06-30

Installed nextflow using [tutorial](https://nf-co.re/docs/usage/tutorials/nf_core_usage_tutorial)

Installed bioconda using [bioconda instructions](https://bioconda.github.io/#usage)
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```

then nf-core and nextflow

Ran these commands
```bash
conda create --name nfcore2023 nf-core
conda install nextflow 
nf-core --help
conda install prettier
```

This worked. Saw `nf-core/tools version 2.8`.





