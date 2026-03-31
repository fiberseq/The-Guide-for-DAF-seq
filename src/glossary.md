# Glossary

**DAF-seq** (Deaminase-Assisted single-molecule chromatin Fiber sequencing): A method for single-molecule footprinting at near-nucleotide resolution that simultaneously profiles chromatin states and DNA sequence. It uses cytosine deamination on intact nuclei to stencil protein occupancy along individual DNA fibers.

**SsDddA**: A nonspecific double-stranded DNA cytidine deaminase from *Simiaoa sunii*. In DAF-seq, SsDddA is applied to intact nuclei where it deaminates accessible (non-protein-bound) cytosines to uracils, which appear as C-to-T transitions after sequencing.

**DddI**: A protein inhibitor of DddA-family deaminases. In DAF-seq, DddI is added at a 5-fold molar excess over SsDddA to stop the deamination reaction.

**UNG inhibitor**: Uracil-N-glycosylase inhibitor (UGI). Added before the deamination step to prevent endogenous UNG from removing uracils created by SsDddA, which would cause DNA strand breaks and data loss.

**scDAF-seq**: Single-cell DAF-seq. A variant of DAF-seq that uses primary template-directed amplification (PTA) to enable single-cell chromatin fiber profiling.

**Decorated BAM**: A BAM file in which full-length DAF-seq reads have been assigned a top or bottom strand designation based on deamination patterns (C-to-T for top strand, G-to-A for bottom strand). Strand designation is stored in the `st` BAM tag.

**Chimera**: A sequencing read that contains deamination signal from both strands, indicated by a mixture of C-to-T and G-to-A conversions. Chimeric reads are filtered using a configurable cutoff (default: 90% single-strand signal).

**Full-length read**: A read that spans the entire targeted amplicon (within a configurable end tolerance, default 30 bp). Only full-length reads are used for strand designation and downstream analysis.

**Consensus BAM** (PacBio only): A BAM file containing multiple-sequence-alignment (MSA) consensus sequences built from groups of PCR duplicate reads. Consensus generation improves accuracy of deamination calls.

**fibertools**: A suite of command-line tools for analyzing single-molecule chromatin fiber data. The `ddda-to-m6a` subcommand converts DAF-seq deamination marks into m6A-equivalent format for compatibility with Fiber-seq analysis tools, and `add-nucleosomes` infers nucleosome positions from the resulting data.
