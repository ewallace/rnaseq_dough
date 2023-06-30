# notes.md

Progress updates on the analysis.

# 2023-06-30

Set out to install nf-core using [nf-core usage tutorial](https://nf-co.re/docs/usage/tutorials/nf_core_usage_tutorial)

First, installed bioconda using [bioconda instructions](https://bioconda.github.io/#usage)

```bash
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```

Next, installed nf-core and nextflow

Ran these commands:

```bash
conda create --name nfcore2023 nf-core
conda install nextflow 
nf-core --help
conda install prettier
```

This worked. Saw `nf-core/tools version 2.8`.

If I did this again, I would want to just install in one line
```bash
conda create --name nf-core-2023 nf-core=2.8 nextflow=23.04 prettier=2.8
```

Next pulling rna-seq. First I tried from the tutorial site:

```
nf-core launch nf-core/rnaseq -r 3.12.0
```

This was very slow on `INFO   Downloading workflow: nf-core/rnaseq (3.12.0)` step, from wifi. After ~5min without update I cancelled, instead going for:

```
nextflow pull rnaseq
nextflow pull nf-core/rnaseq -revision 3.12.0
```

This got stuck too. Not sure why. 






