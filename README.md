# DADA2 Pipeline for 16S Microbiome Analysis

Processes raw 16S rRNA paired-end reads with the **DADA2** pipeline to infer ASVs, remove chimeras, and assign taxonomy. Builds a **phyloseq** object for downstream diversity, composition, and differential abundance analyses.

---

## Features
- Quality filtering/trimming, error learning, ASV inference, and paired-read merging
- Chimera removal and taxonomy assignment (GTDB)
- `phyloseq` object construction with sample metadata
- Read tracking across the pipeline
- Example visualizations (kingdom/phylum composition, top genera, alpha/beta diversity)
- Export of relative-abundance ASV table (tidy, sample-wide)

---

## Requirements

- **R ≥ 4.2**
- R packages: `dada2`, `tidyr`, `ggplot2`, `tidyverse`, `mecodev`, `phyloseq`, `microeco`, `MiscMetabar`, `file2meco`, `dplyr`, `ampvis2`
- Reference taxonomy file (example used):  
  `GTDB_bac120_arc53_ssu_r220_fullTaxo.fa.gz`
- Input FASTQ structure: paired-end files with patterns `*_R1_001.fastq.gz` and `*_R2_001.fastq.gz`

Install packages (example):
```r
install.packages(c("tidyr","ggplot2","tidyverse","dplyr"))
# From Bioc or GitHub as needed:
# BiocManager::install(c("dada2","phyloseq"))
# remotes::install_github("ChiLiubio/microeco")
# remotes::install_github("bcm-uga/MiscMetabar")
# remotes::install_github("ChiLiubio/file2meco")
# install.packages("ampvis2")
