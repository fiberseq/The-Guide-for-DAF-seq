# The Guide to DAF-seq

DAF-seq (Deaminase-Assisted single-molecule chromatin Fiber sequencing) is a method that enables single-molecule footprinting at near-nucleotide resolution while synchronously profiling single-molecule chromatin states and DNA sequence. It leverages SsDddA, a nonspecific cytidine deaminase from *Simiaoa sunii*, to selectively stencil single-molecule protein occupancy on intact nuclei. DAF-seq is compatible with both PacBio HiFi and Oxford Nanopore sequencing platforms, and a single-cell version (scDAF-seq) is also available.

The method is described in:

> Swanson, Mao, Mallory, Vollger, Bohaczuk, Oliveira, Lyon, Ranchalis, Parmalee, Cohen, Bennett & Stergachis. *Mapping single-cell diploid chromatin fiber architectures using DAF-seq.* Nature Biotechnology (2025). [DOI: 10.1038/s41587-025-02914-3](https://doi.org/10.1038/s41587-025-02914-3)

## Quick start

- **Running the experiment?** Start with the [DAF-seq Protocol](protocol/protocol.md) for the complete wet lab workflow.
- **Analyzing data?** Jump to the [DAF-QC Pipeline](drylab/daf-qc.md) for computational setup and quality control.
- **New to DAF-seq?** See the [Glossary](glossary.md) for definitions of key terms.

## What's here

**Wet Lab**
- [DAF-seq Protocol](protocol/protocol.md) -- Complete protocol for nuclei isolation, on-nuclei cytosine deamination, and DNA extraction
- [Primer Design](protocol/primer-design.md) -- Guidelines for designing primers for targeted DAF-seq
- [Protein Purification](protocol/protein-purification.md) -- Purification protocols for SsDddA and DddI

**Dry Lab**
- [DAF-QC Pipeline](drylab/daf-qc.md) -- Snakemake pipeline for quality control and initial processing of DAF-seq data

**Reference**
- [Glossary](glossary.md) -- Definitions of key DAF-seq terms and concepts
- [Cite](cite.md) -- Citation information and BibTeX entry

## Contributing

**You can help improve this guide! Click the edit button (<i class="fa fa-edit"></i>) in the top right of any page to suggest changes.**

For questions or contributions, see the relevant GitHub repositories:
- [DAF-seq Manuscript](https://github.com/StergachisLab/DAF-seq-Manuscript) -- Analysis code and supplementary materials
- [DAF-QC-SMK](https://github.com/StergachisLab/DAF-QC-SMK) -- QC pipeline source code and documentation
- [This website](https://github.com/fiberseq/dafseq.github.io) -- Source for these documentation pages
