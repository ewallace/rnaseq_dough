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

Eventually

<details>

<summary> `nextflow run nf-core/rnaseq -r 3.12.0 -profile test --outdir test-out` </summary>
  
```

(nfcore2023) ewallac2@sce-bio-c06313 rnaseq_dough % nextflow run nf-core/rnaseq -r 3.12.0 -profile test --outdir test-out
N E X T F L O W  ~  version 23.04.1
Pulling nf-core/rnaseq ...
 downloaded from https://github.com/nf-core/rnaseq.git
Launching `https://github.com/nf-core/rnaseq` [elated_saha] DSL2 - revision: 3bec2331ca [3.12.0]


------------------------------------------------------
                                        ,--./,-.
        ___     __   __   __   ___     /,-._.--~'
  |\ | |__  __ /  ` /  \ |__) |__         }  {
  | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                        `._,._,'
  nf-core/rnaseq v3.12.0-g3bec233
------------------------------------------------------
Core Nextflow options
  revision                  : 3.12.0
  runName                   : elated_saha
  launchDir                 : /Users/ewallac2/Repos/rnaseq_dough
  workDir                   : /Users/ewallac2/Repos/rnaseq_dough/work
  projectDir                : /Users/ewallac2/.nextflow/assets/nf-core/rnaseq
  userName                  : ewallac2
  profile                   : test
  configFiles               : /Users/ewallac2/.nextflow/assets/nf-core/rnaseq/nextflow.config

Input/output options
  input                     : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/samplesheet/v3.10/samplesheet_test.csv
  outdir                    : test-out

UMI options
  umitools_bc_pattern       : NNNN

Read filtering options
  bbsplit_fasta_list        : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/bbsplit_fasta_list.txt
  skip_bbsplit              : false

Reference genome options
  fasta                     : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genome.fasta
  gtf                       : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genes.gtf.gz
  gff                       : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genes.gff.gz
  transcript_fasta          : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/transcriptome.fasta
  additional_fasta          : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/gfp.fa.gz
  hisat2_index              : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/hisat2.tar.gz
  rsem_index                : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/rsem.tar.gz
  salmon_index              : https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/salmon.tar.gz

Alignment options
  pseudo_aligner            : salmon

Institutional config options
  config_profile_name       : Test profile
  config_profile_description: Minimal test dataset to check pipeline function

Max job request options
  max_cpus                  : 2
  max_memory                : 6.GB
  max_time                  : 6.h

!! Only displaying parameters that differ from the pipeline defaults !!
------------------------------------------------------
If you use nf-core/rnaseq for your analysis please cite:

* The pipeline
  https://doi.org/10.5281/zenodo.1400710

* The nf-core framework
  https://doi.org/10.1038/s41587-020-0439-x

* Software dependencies
  https://github.com/nf-core/rnaseq/blob/master/CITATIONS.md
------------------------------------------------------
WARN: ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  Both '--gtf' and '--gff' parameters have been provided.
  Using GTF file as priority.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
WARN: ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  '--transcript_fasta' parameter has been provided.
  Make sure transcript names in this file match those in the GFF/GTF file.

  Please see:
  https://github.com/nf-core/rnaseq/issues/753
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
executor >  local (1)
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX   -
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
executor >  local (2)
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF           -
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX   -
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
executor >  local (2)
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF           -
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX   -
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
executor >  local (2)
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF           [  0%] 0 of 1
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX   -
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
executor >  local (2)
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF           [  0%] 0 of 1
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX   [  0%] 0 of 1
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
executor >  local (4)
[d1/7ec538] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF (genes... [  0%] 0 of 1
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[34/870595] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDE... [  0%] 0 of 1
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
executor >  local (4)
[d1/7ec538] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF (genes... [100%] 1 of 1 ✔
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[34/870595] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDE... [  0%] 0 of 1
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
executor >  local (4)
[d1/7ec538] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF (genes... [100%] 1 of 1 ✔
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[34/870595] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDE... [  0%] 0 of 1
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUALIMAP_RNASEQ                     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DUPRADAR                            -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_BAMSTAT             -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INNERDISTANCE       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INFEREXPERIMENT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONANNOTATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONSATURATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDISTRIBUTION    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDUPLICATION     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_QUANT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TX2GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TXIMPORT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_L... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_S... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_TRANSC... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_SALMON                    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:CUSTOM_DUMPSOFTWAREVERSIONS         -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC                             -
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/salmon.tar.gz
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genes.gtf.gz
WARN: Task runtime metrics are not reported when using macOS without a container engine
ERROR ~ Error executing process > 'NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)

Caused by:
  Process `NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)` terminated with an error exit status (1)

Command executed:

  mkdir salmon
  
  ## Ensures --strip-components only applied when top level of tar contents is a directory
  ## If just files or multiple directories, place all in prefix
  if [[ $(tar -taf salmon.tar.gz | grep -o -P "^.*?\/" | uniq | wc -l) -eq 1 ]]; then
      tar \
          -C salmon --strip-components 1 \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  else
      tar \
          -C salmon \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  fi
  
executor >  local (4)
[d1/7ec538] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF (genes... [100%] 1 of 1 ✔
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[34/870595] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDE... [100%] 1 of 1, failed: 1 ✘
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUALIMAP_RNASEQ                     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DUPRADAR                            -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_BAMSTAT             -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INNERDISTANCE       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INFEREXPERIMENT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONANNOTATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONSATURATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDISTRIBUTION    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDUPLICATION     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_QUANT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TX2GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TXIMPORT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_L... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_S... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_TRANSC... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_SALMON                    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:CUSTOM_DUMPSOFTWAREVERSIONS         -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC                             -
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/salmon.tar.gz
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genes.gtf.gz
Execution cancelled -- Finishing pending tasks before exit
WARN: Task runtime metrics are not reported when using macOS without a container engine
ERROR ~ Error executing process > 'NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)

Caused by:
  Process `NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)` terminated with an error exit status (1)

Command executed:

  mkdir salmon
  
  ## Ensures --strip-components only applied when top level of tar contents is a directory
  ## If just files or multiple directories, place all in prefix
  if [[ $(tar -taf salmon.tar.gz | grep -o -P "^.*?\/" | uniq | wc -l) -eq 1 ]]; then
      tar \
          -C salmon --strip-components 1 \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  else
      tar \
          -C salmon \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  fi
  
executor >  local (4)
[d1/7ec538] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF (genes... [100%] 1 of 1 ✔
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[34/870595] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDE... [100%] 1 of 1, failed: 1 ✘
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUALIMAP_RNASEQ                     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DUPRADAR                            -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_BAMSTAT             -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INNERDISTANCE       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INFEREXPERIMENT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONANNOTATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONSATURATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDISTRIBUTION    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDUPLICATION     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_QUANT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TX2GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TXIMPORT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_L... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_S... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_TRANSC... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_SALMON                    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:CUSTOM_DUMPSOFTWAREVERSIONS         -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC                             -
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/salmon.tar.gz
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genes.gtf.gz
Execution cancelled -- Finishing pending tasks before exit
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genome.fasta
WARN: Task runtime metrics are not reported when using macOS without a container engine
ERROR ~ Error executing process > 'NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)

Caused by:
  Process `NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)` terminated with an error exit status (1)

Command executed:

  mkdir salmon
  
  ## Ensures --strip-components only applied when top level of tar contents is a directory
  ## If just files or multiple directories, place all in prefix
  if [[ $(tar -taf salmon.tar.gz | grep -o -P "^.*?\/" | uniq | wc -l) -eq 1 ]]; then
      tar \
          -C salmon --strip-components 1 \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  else
      tar \
          -C salmon \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  fi
  
executor >  local (4)
[d1/7ec538] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF (genes... [100%] 1 of 1 ✔
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[34/870595] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDE... [100%] 1 of 1, failed: 1 ✘
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUALIMAP_RNASEQ                     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DUPRADAR                            -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_BAMSTAT             -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INNERDISTANCE       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INFEREXPERIMENT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONANNOTATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONSATURATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDISTRIBUTION    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDUPLICATION     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_QUANT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TX2GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TXIMPORT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_L... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_S... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_TRANSC... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_SALMON                    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:CUSTOM_DUMPSOFTWAREVERSIONS         -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC                             -
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/salmon.tar.gz
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genes.gtf.gz
Execution cancelled -- Finishing pending tasks before exit
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genome.fasta
-[nf-core/rnaseq] Pipeline completed with errors-
WARN: Task runtime metrics are not reported when using macOS without a container engine
ERROR ~ Error executing process > 'NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)

Caused by:
  Process `NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)` terminated with an error exit status (1)

Command executed:

  mkdir salmon
  
  ## Ensures --strip-components only applied when top level of tar contents is a directory
  ## If just files or multiple directories, place all in prefix
  if [[ $(tar -taf salmon.tar.gz | grep -o -P "^.*?\/" | uniq | wc -l) -eq 1 ]]; then
      tar \
          -C salmon --strip-components 1 \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  else
      tar \
          -C salmon \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  fi
  
executor >  local (4)
[d1/7ec538] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF (genes... [100%] 1 of 1 ✔
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[34/870595] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDE... [100%] 1 of 1, failed: 1 ✘
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUALIMAP_RNASEQ                     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DUPRADAR                            -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_BAMSTAT             -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INNERDISTANCE       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INFEREXPERIMENT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONANNOTATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONSATURATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDISTRIBUTION    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDUPLICATION     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_QUANT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TX2GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TXIMPORT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_L... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_S... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_TRANSC... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_SALMON                    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:CUSTOM_DUMPSOFTWAREVERSIONS         -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC                             -
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/salmon.tar.gz
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genes.gtf.gz
Execution cancelled -- Finishing pending tasks before exit
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genome.fasta
-[nf-core/rnaseq] Pipeline completed with errors-
WARN: Task runtime metrics are not reported when using macOS without a container engine
ERROR ~ Error executing process > 'NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)

Caused by:
  Process `NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)` terminated with an error exit status (1)

Command executed:

  mkdir salmon
  
  ## Ensures --strip-components only applied when top level of tar contents is a directory
  ## If just files or multiple directories, place all in prefix
  if [[ $(tar -taf salmon.tar.gz | grep -o -P "^.*?\/" | uniq | wc -l) -eq 1 ]]; then
      tar \
          -C salmon --strip-components 1 \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  else
      tar \
          -C salmon \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  fi
  
executor >  local (4)
[d1/7ec538] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_GTF (genes... [100%] 1 of 1 ✔
[13/cc3e80] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GUNZIP_ADDITIONAL... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CAT_ADDITIONAL_FASTA [  0%] 0 of 1
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:GTF2BED              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:CUSTOM_GETCHROMSIZES -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:BBMAP_BBSPLIT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:STAR_GENOMEGENERATE  -
[34/870595] process > NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDE... [100%] 1 of 1, failed: 1 ✘
[75/bc1a66] process > NFCORE_RNASEQ:RNASEQ:INPUT_CHECK:SAMPLESHEET_CHECK (s... [100%] 1 of 1 ✔
[-        ] process > NFCORE_RNASEQ:RNASEQ:CAT_FASTQ                           -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:FQ_SUB... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_SUBSAMPLE_FQ_SALMON:SALMON... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:FASTQ_FASTQC_UMITOOLS_TRIMGALORE... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BBMAP_BBSPLIT                       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:STAR_ALIGN               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:ALIGN_STAR:BAM_SORT_STATS_SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_QUANT   -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TX2GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_TXIM... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_GENE -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_G... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_STAR_SALMON:SALMON_SE_T... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_STAR_SALMON               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:PICARD... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:SAMTOO... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_MARKDUPLICATES_PICARD:BAM_ST... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:STRINGTIE_STRINGTIE                 -
[-        ] process > NFCORE_RNASEQ:RNASEQ:SUBREAD_FEATURECOUNTS               -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC_CUSTOM_BIOTYPE              -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDTOOLS_GENOMECOV                  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BEDGRAPH_BEDCLIP_BEDGRAPHTOBIGWI... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUALIMAP_RNASEQ                     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DUPRADAR                            -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_BAMSTAT             -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INNERDISTANCE       -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_INFEREXPERIMENT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONANNOTATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_JUNCTIONSATURATION  -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDISTRIBUTION    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:BAM_RSEQC:RSEQC_READDUPLICATION     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_QUANT        -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TX2GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_TXIMPORT     -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE      -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_L... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_GENE_S... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:QUANTIFY_SALMON:SALMON_SE_TRANSC... -
[-        ] process > NFCORE_RNASEQ:RNASEQ:DESEQ2_QC_SALMON                    -
[-        ] process > NFCORE_RNASEQ:RNASEQ:CUSTOM_DUMPSOFTWAREVERSIONS         -
[-        ] process > NFCORE_RNASEQ:RNASEQ:MULTIQC                             -
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/salmon.tar.gz
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genes.gtf.gz
Execution cancelled -- Finishing pending tasks before exit
Staging foreign file: https://raw.githubusercontent.com/nf-core/test-datasets/rnaseq/reference/genome.fasta
-[nf-core/rnaseq] Pipeline completed with errors-
WARN: Task runtime metrics are not reported when using macOS without a container engine
ERROR ~ Error executing process > 'NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)

Caused by:
  Process `NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX (salmon.tar.gz)` terminated with an error exit status (1)

Command executed:

  mkdir salmon
  
  ## Ensures --strip-components only applied when top level of tar contents is a directory
  ## If just files or multiple directories, place all in prefix
  if [[ $(tar -taf salmon.tar.gz | grep -o -P "^.*?\/" | uniq | wc -l) -eq 1 ]]; then
      tar \
          -C salmon --strip-components 1 \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  else
      tar \
          -C salmon \
          -xavf \
           \
          salmon.tar.gz \
          --no-same-owner
  fi
  
  cat <<-END_VERSIONS > versions.yml
  "NFCORE_RNASEQ:RNASEQ:PREPARE_GENOME:UNTAR_SALMON_INDEX":
      untar: $(echo $(tar --version 2>&1) | sed 's/^.*(GNU tar) //; s/ Copyright.*$//')
  END_VERSIONS

Command exit status:
  1

Command output:
  (empty)

Command error:
  grep: invalid option -- P
  usage: grep [-abcdDEFGHhIiJLlMmnOopqRSsUVvwXxZz] [-A num] [-B num] [-C[num]]
  	[-e pattern] [-f file] [--binary-files=value] [--color=when]
  	[--context[=num]] [--directories=action] [--label] [--line-buffered]
  	[--null] [pattern] [file ...]
  tar: Option -a is not permitted in mode -t
  tar: Option -a is not permitted in mode -x

Work dir:
  /Users/ewallac2/Repos/rnaseq_dough/work/34/8705953d677984f7e81a941e14e399

Tip: view the complete command output by changing to the process work dir and entering the command `cat .command.out`

 -- Check '.nextflow.log' file for details

```

</details>








