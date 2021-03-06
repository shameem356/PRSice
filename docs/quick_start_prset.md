# Background
A new feature of PRSice is the ability to perform set base/pathway based analysis. This new feature is called PRSet.

Paper on PRSet currently under preparation.

!!! Important
    PRSet is currently under active development. Notably, the current version of PRSet only provides self-contained pathway results, which eg. do not account for pathway size. For now other leading pathway approaches (eg. [MAGMA](https://ctg.cncr.nl/software/magma)) might be more powerful for identification of causal pathways.

# Preparation
PRSet is based on [PRSice](quick_start.md), with additional input requirements

## Input
- **PRSice.R file**: A wrapper for the PRSice binary and for plotting
- **PRSice binary file**: Perform all analysis except plotting
- **Base data set**: GWAS summary results, which the PRS is based on
- **Target data set**: Raw genotype data of "target phenotype". Can be in the form of  [PLINK binary](https://www.cog-genomics.org/plink2/formats#bed) or [BGEN](http://www.well.ox.ac.uk/~gav/bgen_format/)
## PRSet Specific Input
- **Bed file(s)**: Bed file(s) containing region of genes within a gene set; or
- **MSigDB file**: File containing name of each gene sets and the ID of genes within the
gene set on each individual line. If MSigDB is provided, GTF file is required.
- **GTF file**: A file contain the genome boundary of each individual gene

# Running PRSet

In most case, PRSet can simply be run using the following command, assuming the
PRSice binary is located in `($HOME)/PRSice/bin/` and the working directory is `($HOME)/PRSice`

## With MSigDB data
Assuming a MSigDB file (*set.txt*) is [downloaded](http://software.broadinstitute.org/gsea/msigdb/) and a gene gtf file (gene.gtf) from [Ensemble](http://www.ensembl.org/index.html) is available, PRSet can then be performed using: 

``` bash hl_lines="7 8 9"
Rscript PRSice.R \
    --prsice ./bin/PRSice \
    --base TOY_BASE_GWAS.assoc \
    --target TOY_TARGET_DATA \
    --binary-target T \
    --thread 1 \
    --gtf gene.gtf \
    --msigdb set.txt \
    --multi-plot 10
```

This will perform PRSet analysis and generate the multi-set plot with the top 10 gene sets

## With Bed Files
Alternatively, if a list of bed files are available, e.g. *A.bed,B.bed*, PRSet can be performed by running

``` bash hl_lines="7 8"
Rscript PRSice.R \
    --prsice ./bin/PRSice \
    --base TOY_BASE_GWAS.assoc \
    --target TOY_TARGET_DATA \
    --binary-target T \
    --thread 1 \
    --bed A.bed,B.bed \
    --multi-plot 10
```

!!! Note
    Both bed and GTF+MSigDB input can be used together
