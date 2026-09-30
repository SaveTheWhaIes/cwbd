# Course Description
This practical course will give you a hands-on introduction to the innovative landscape of computational workflows in biomedical research, with a specialized focus on Nextflow and nf-core. This course is designed to equip participants with the essential tools and techniques required to effectively analyze complex biological data.

Key Topics Covered:
(1) Introduction to computational workflows with a focus on Nextflow and nf-core: Understanding the fundamentals
(2) Building scalable and reproducible workflows
(3) Data preprocessing and quality control in bioinformatics using workflows
(4) Concepts for the implementation of workflows to leverage cloud computing resources and other infrastructures

What you will Gain:

(1) Practical experience in designing and implementing computational workflows
(2) Proficiency in utilizing Nextflow and nf-core for bioinformatics analysis
(3) Skills in data preprocessing, quality control, and integration
(4) Ability to optimize workflows for scalability and reproducibility and specifically to reprocess publicly available data

Will have the chance to work independently or in teams on research projects, implementing and using computational workflows. You will present the results of your research and implementation project (about 20 minutes) and write a short scientific paper (approx. 2000 words).
Where: M3 research center, Otfried-Müller-Str. 37, Seminar Room Level 2.

# Required Setup

Make sure you have the following installed on your local machine:
````
# install and setup up on your machine:
conda
docker

# install via Conda:
nextflow>=26.04
nf-core>=4.1
python>=3.9
pandas
matplotlib
seaborn
````

You need to install microconda and docker on your machine, then you can install the other requirements via conda.

# Daily log

## Day 1 (2026-09-28): nf-core basics
First contact with nf-core: what it is and why its guidelines matter, then nf-core/differentialabundance 2.0.0 on the test profile to see how Nextflow reruns, caches (`-resume`) and loses its cache when `work/` is deleted. The test data (hND6 vs mCherry) barely separates; the only clear signal is immunoglobulin genes.

Notebook: [day_01/day_01.ipynb](day_01/day_01.ipynb)

## Day 2 (2026-09-29): Study, raw data and read QC
The study (Mitsi et al. 2023, oxycodone withdrawal with and without neuropathic pain, 2 x 2 design, 4 NAc samples per group). Part 1 tidies the run table, checks depth (Oxy runs about 10 % shallower) and downloads the two smallest runs with nf-core/fetchngs. Part 2 runs nf-core/rnaseq 3.27.0 (HISAT2 + Salmon) on them and reads the QC: SNI_Oxy is a low complexity library, Sham_Oxy carries many intronic reads. The tutors' run of all 16 samples reveals human rRNA in C4, F3 and B4 and mouse rRNA in F1 and C2.

Notebooks: [day_02/day_02_part1.ipynb](day_02/day_02_part1.ipynb), [day_02/day_02_part2.ipynb](day_02/day_02_part2.ipynb)

## Day 3 (2026-09-30): Differential expression
nf-core/differentialabundance 2.0.0 on the provided count matrix, once with all 16 samples and once without C4, F3, B4, at the paper cutoff (p < 0.05, |log2FC| > 0.5). Removing the contaminated samples moves the DEG counts towards the paper (clean 13: SNI-Sal 2042, Sham-Oxy 1531, SNI-Oxy 1198 vs paper 1457, 2609, 1012) and the shared Venn core to 577 (paper 420). Only a few hundred genes survive padj < 0.05.

Notebook: [day_03/day_03.ipynb](day_03/day_03.ipynb)
