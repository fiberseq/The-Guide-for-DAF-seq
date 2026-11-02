# FiberHMM

[FiberHMM](https://github.com/fiberseq/FiberHMM) is a Hidden Markov Model toolkit for calling chromatin footprints from single-molecule DNA modification data. It supports DAF-seq (DddA and DddB) as well as Fiber-seq (PacBio and Nanopore Hia5), and emits nucleosomes, methylase-sensitive patches (MSPs), and sub-nucleosomal TF/Pol II footprints in [fibertools](https://github.com/fiberseq/fibertools-rs)-compatible BAMs.

For DAF-seq, FiberHMM is a native nucleosome and footprint caller that runs directly on deaminase data with DAF-trained HMM emissions, adds a log-likelihood-ratio recaller for transcription factor footprints, and writes spec-compliant [Molecular-annotation](https://github.com/fiberseq/Molecular-annotation-spec) tags. This page covers installation, inputs, and the recommended one-command workflow.

Install the latest release from [PyPI](https://pypi.org/project/fiberhmm/). FiberHMM and [FiberBrowser](fiberbrowser.md) are described in our [bioRxiv preprint](https://www.biorxiv.org/content/10.64898/2026.10.29.762797v1); please cite it if you use FiberHMM.

## Getting started

Install from PyPI:

```bash
pip install fiberhmm
```

Optional dependencies that are worth installing:

```bash
pip install numba        # ~10x faster HMM computation
pip install matplotlib   # --stats visualization
pip install h5py         # HDF5 posteriors export
```

For bigBed output, install [`bedToBigBed`](https://hgdownload.soe.ucsc.edu/admin/exe/) from UCSC tools.

Pre-trained models for DddA and DddB are bundled with the package; no separate download is required.

## Inputs

FiberHMM operates on aligned DAF-seq BAMs from the [DAF-QC pipeline](daf-qc.md) (or any equivalent alignment workflow). In DAF mode, the caller needs to know which positions on each read are C-to-T or G-to-A conversions. It auto-detects this per read from any of:

- **R/Y IUPAC codes in the stored sequence**, written by `fiberhmm-daf-encode`.
- **MD tag** on a raw aligned BAM (produced by `minimap2 --MD` or `samtools calmd`). Parsed on the fly; no preprocessing step needed.
- **MM/ML tags** encoding deaminated C/G positions as base modifications.
- **`--reference ref.fa`**, used as a fallback when none of the above are present.

At least one of these must be present on the input BAM.

## Usage

`fiberhmm-call` runs the whole caller in one pass: HMM segmentation, nucleosome refinement and TF footprint refinement ([how it works](daf-footprinting.md)). Pick the enzyme; the bundled model and defaults follow.

```bash
# DddB (aligned with MD tags, e.g. minimap2 --MD)
fiberhmm-call -i aligned.bam -o calls.bam --enzyme dddb -c 8 --region-parallel

# SsDddA (single-cell DAF-seq)
fiberhmm-call -i aligned.bam -o calls.bam --enzyme ddda -c 8 --region-parallel
```

`--region-parallel` needs a coordinate-sorted, indexed input and scales with `-c`. The output is sorted and indexed.

For SsDddA, nucleosomes are placed by the phase-aware caller, which keeps the rotationally phased deaminations inside nucleosomes rather than reading them as linkers. CpGs are treated as methylated by default. To use CpG evidence where it is informative, classify whole CpG islands with `fiberhmm-tag-m5c` and call again; the second call uses CpGs only inside islands called unmethylated:

```bash
fiberhmm-call -i aligned.bam -o calls.bam --enzyme ddda -c 8 --region-parallel
fiberhmm-tag-m5c -i calls.bam -o islands.bam -r genome.fa --enzyme ddda
fiberhmm-call -i islands.bam -o calls.cpg.bam --enzyme ddda -c 8 --region-parallel
```

For paired single-cell strands (the C-to-T and G-to-A copies of one fiber), `fiberhmm-pair` joins the two strands of each duplex so they are called together ([duplex calling](daf-footprinting.md#duplex-calibration-and-calling)).

From raw reads of a plasmid or amplicon run (for example a Plasmidsaurus Nanopore run), `fiberhmm-pipeline` aligns, calls and runs QC in one command:

```bash
fiberhmm-pipeline reads.fastq.gz --reference construct.dna --enzyme dddb -o my_run/
```

## Key outputs

`fiberhmm-call` writes a tagged BAM that FiberBrowser, FIRE and fibertools read directly.

- **Molecular-annotation tags** (`MA`, `AQ`): every call, in `nuc.QQQ` (nucleosomes), `msp.` (accessible patches) and `tf.QQQ` (TF, Pol II and other sub-nucleosomal footprints) groups, with per-call quality bytes: the LLR-based score and left and right edge sharpness. See the [spec](https://github.com/fiberseq/Molecular-annotation-spec) for the encoding.
- **Legacy tags** (`ns`/`nl`, `as`/`al`): nucleosome and MSP starts and lengths, for tools that read only those. TF footprints are in `MA` only.
- **Footprint threshold**: TF footprints are called at LLR 5 for every chemistry, the lowest integer threshold at which calls in accessible controls stay below 2%. `--min-llr` overrides it.

### Extract to bigBed

For a compact copy of the calls for genome browsers and downstream analysis:

```bash
fiberhmm-extract -i calls.bam --nucleosome --msp --tf
```

This writes bigBed files next to the BAM (`--bed-only` for plain BED; UCSC `bedToBigBed` must be installed for bigBed).

## Choosing options

| Situation | Command |
|---|---|
| DddB, sorted and indexed BAM | `fiberhmm-call --enzyme dddb --region-parallel` |
| SsDddA, sorted and indexed BAM | `fiberhmm-call --enzyme ddda --region-parallel` |
| SsDddA with CpG-island methylation | `fiberhmm-call`, then `fiberhmm-tag-m5c`, then `fiberhmm-call` again |
| Paired single-cell strands | `fiberhmm-pair` |
| FIRE element calls afterwards | pipe `fiberhmm-call -o -` into `ft fire - final.bam` |
| Raw reads of a plasmid or amplicon run | `fiberhmm-pipeline` |

The [FiberHMM documentation](https://fiberseq.github.io/FiberHMM/) covers every command and option, including Hia5 Fiber-seq, training new models and posterior export.

## Further reading

- [FiberHMM repository and README](https://github.com/fiberseq/FiberHMM)
- [Molecular-annotation spec](https://github.com/fiberseq/Molecular-annotation-spec) for the `MA`/`AQ` tag schema
- [fibertools-rs](https://github.com/fiberseq/fibertools-rs) for downstream FIRE scoring and extraction
