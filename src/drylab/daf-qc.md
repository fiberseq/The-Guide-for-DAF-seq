# DAF-QC Pipeline

[DAF-QC-SMK](https://github.com/StergachisLab/DAF-QC-SMK) is a Snakemake pipeline for quality control and initial processing of DAF-seq sequencing reads. It supports both PacBio HiFi and Oxford Nanopore platforms. This page covers installation, usage, and key outputs. For the wet lab steps that precede this pipeline, see the [DAF-seq Protocol](../protocol/protocol.md).

## Getting started

The pipeline uses [pixi](https://pixi.sh/latest/) for environment management. Clone the repository and install:

```bash
git clone https://github.com/StergachisLab/DAF-QC-SMK.git
cd DAF-QC-SMK
pixi install
```

### Verify the installation

A test dataset (human chr8, hg38) is bundled with the repository. Run it to confirm everything is working before processing your own data:

```bash
pixi run test
```

If you encounter errors, please run the test case before contacting the developers, as it helps with troubleshooting.

## Usage

Run the pipeline with pixi:

```bash
pixi run snakemake --configfile config/config.yaml
```

For SLURM clusters, specify a profile:

```bash
pixi run snakemake --configfile config/config.yaml --profile profiles/slurm-executor
```

You can also run the pipeline from a different directory using `--manifest-path`:

```bash
pixi run --manifest-path /path/to/DAF-QC-SMK/pixi.toml snakemake --configfile config/config.yaml
```

## Inputs

The pipeline requires two configuration files:

### Sample table (`config.tbl`)

A tab-separated table with sample name, BAM/FASTQ path, and targeted regions:

```
sample	file	regs
test    test.bam    chr8:144415767-144417958
```

For PacBio BAM inputs, files should contain either unaligned reads or primary reads only (for compatibility with `pbmarkdup` during consensus generation). See `config/config.tbl` in the repository for a template.

### Configuration file (`config.yaml`)

Specifies paths to the sample table and reference genome, sequencing platform, and optional parameters:

```yaml
ref: /path/to/genome.fa
manifest: config/config.tbl
platform: pacbio  # 'pacbio' or 'ont'

# Optional (both platforms)
chimera_cutoff: 0.9
min_deamination_count: 50
end_tolerance: 30
decorated_samplesize: 5000

# PacBio-specific
consensus: True
consensus_min_reads: 3

# ONT-specific
is_fastq: False
```

See `config/config.yaml` in the repository for the full list of options with descriptions.

## Key outputs

- **Aligned BAMs**: Primary, supplementary, and unaligned reads with PCR duplicates marked (`du` and `ds` tags).
- **Decorated BAMs**: Full-length reads with top/bottom strand designation (C-to-T as top strand, G-to-A as bottom strand). Strand stored in the `st` tag.
- **Consensus BAMs** (PacBio only): MSA consensus of full-length, strand-designated reads. The `dc` tag indicates the number of reads used to construct each consensus.
- **QC metrics**: Targeting efficiency, deamination rates (overall and by 2-bp sequence context), strand calling, enzyme bias, and mutation rates.
- **HTML dashboard**: `results/{sample_name}/qc/{sample_name}.dashboard.html` with all QC plots. The dashboard is self-contained (plots are embedded), so you can copy a single file for sharing or local viewing.

## Downstream analysis with fibertools

After QC, DAF-seq data can be further processed with [fibertools](https://github.com/fiberseq/fibertools-rs) (`ft`) for chromatin fiber analysis:

1. **`ft ddda-to-m6a`**: Converts DAF-seq deamination marks (C-to-T / G-to-A) into m6A-equivalent format, enabling compatibility with the Fiber-seq analysis ecosystem.
2. **`ft add-nucleosomes`**: Infers nucleosome positions from the converted deamination data.

These steps allow you to use the full suite of Fiber-seq visualization and analysis tools on DAF-seq data. See the [fibertools documentation](https://fiberseq.github.io) for details.

## Further reading

See the [DAF-QC-SMK README](https://github.com/StergachisLab/DAF-QC-SMK#readme) for full details on all configuration options, output file formats, and BAM tag specifications.
