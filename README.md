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
```

Data Layout
project/
├─ script.R                         # This pipeline script
├─ metadata.csv                     # Sample metadata (row names = SampleID)
├─ GTDB_bac120_arc53_ssu_r220_fullTaxo.fa.gz
└─ 16s_datasets/          # FASTQ files
   ├─ SAMPLE1_R1_001.fastq.gz
   ├─ SAMPLE1_R2_001.fastq.gz
   └─ ...


Required metadata fields

SampleID (must match FASTQ sample IDs)

Group (used for grouping/plots; rename or adjust in script if different)

Usage

Set the input path at the top of the script:

path <- "D:/work/OmicsLogic_Workshop/OmisLogic_16s_datasets/"


(Use a POSIX path on macOS/Linux, e.g., "/path/to/OmisLogic_16s_datasets/".)

Run the script in R or as a batch:

Rscript script.R

Outputs

denoising_stats.csv — read counts per sample across steps: input, filtered, denoisedF/R, merged, nonchim

In-session objects:

seqtab, seqtab.nochim — ASV tables (raw and non-chimeric)

taxa — taxonomy table

ps — phyloseq object with counts, taxonomy, and metadata

ps.relative_abundance.all.tsv — wide table of relative abundances with taxonomy columns

Plots Generated (examples)

Quality profiles: plotQualityProfile for a quick QC peek

Composition:

Kingdom-level stacked bars

Phylum-level stacked bars

Top Genera (microeco):

Top-20 genus bar plot

Diversity:

Alpha diversity (Shannon, etc.)

Beta diversity (Bray–Curtis) ordination

Customize themes/facets or add ggsave() calls where needed.

Customization Tips

Truncation/quality thresholds: adjust truncLen, maxEE, truncQ in filterAndTrim()

Threads: set multithread=TRUE where supported for speed

Grouping variable: update "Group" to your metadata column if different

Taxonomy DB: swap the GTDB FASTA for SILVA/RDP if preferred (and adjust path)

Troubleshooting

No / few reads after filtering: relax truncLen or maxEE; verify read quality profiles

Merge failures: ensure adequate overlap between trimmed R1/R2; tweak truncLen

Taxonomy file path: confirm the .fa.gz file exists and is readable

Sample name mismatches: FASTQ sample IDs must match SampleID in metadata.csv

Citation

Please cite the tools you use (examples):

DADA2

phyloseq

microeco

ampvis2

GTDB (if using their taxonomy)
