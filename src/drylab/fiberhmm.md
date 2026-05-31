# FiberHMM

[FiberHMM](https://github.com/fiberseq/FiberHMM) is a Hidden Markov Model toolkit for calling chromatin footprints from single-molecule DNA modification data. It supports DAF-seq (DddA and DddB) as well as Fiber-seq (PacBio and Nanopore Hia5), and emits nucleosomes, methylase-sensitive patches (MSPs), and sub-nucleosomal TF/Pol II footprints in [fibertools](https://github.com/fiberseq/fibertools-rs)-compatible BAMs.

For DAF-seq, FiberHMM is a native nucleosome and footprint caller that runs directly on deaminase data with DAF-trained HMM emissions, adds a log-likelihood-ratio recaller for transcription factor footprints, and writes spec-compliant [Molecular-annotation](https://github.com/fiberseq/Molecular-annotation-spec) tags. This page covers installation, inputs, and the recommended one-command workflow.

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

`fiberhmm-call` is the recommended entry point. It fuses the nucleosome/MSP HMM and the TF recaller into a single in-process pipeline.

### DddA

FiberHMM automatically selects the DddA two-model workflow under the hood (a nucleosome model plus a TF recall pass with an efficiency uplift to match DddA's higher per-position deamination rate).

```bash
fiberhmm-call -i aligned.bam -o recalled.bam \
              --mode daf --enzyme ddda \
              -c 8 --io-threads 16 \
              --region-parallel
```

`--region-parallel` requires a coordinate-sorted and indexed input and scales near-linearly with `--cores` up to the chromosome count. The output is sorted and indexed in place; no separate sort pass is needed.

DddB samples are supported by the same commands with `--enzyme dddb`.

## Key outputs

`fiberhmm-call` writes a tagged BAM that downstream tools like FiberBrowser and Fibertools can read directly.

- **Legacy footprint tags** (`ns`/`nl`, `as`/`al`): nucleosome and MSP starts and lengths, compatible with any tool in the fibertools ecosystem.
- **Molecular-annotation spec tags** (`MA`, `AQ`): per-spec `nuc+Q`, `msp+`, and `tf+QQQ` annotations with LLR-based confidence (`tq`) and edge-sharpness bytes (`el`, `er`) on TF calls. See the [spec](https://github.com/fiberseq/Molecular-annotation-spec) for the encoding.
- **TF/Pol II footprints**: sub-nucleosomal calls (typically 15–80 bp) live in the `tf+QQQ` annotation of `MA`/`AQ`. For DAF-seq, the recaller uses a tuned `--min-llr` (5.0 for DddA, 4.0 for DddB) selected automatically by `--enzyme`.

### Extract to bigBed

For a smaller-filesize representation of the call set for downstream analysis and [FiberBrowser](https://github.com/fiberseq/FiberBrowser), convert the tagged BAM:

```bash
fiberhmm-extract -i recalled.bam --footprint --msp --tf --bigbed
```

## Choosing options

| Situation | Command |
|---|---|
| Default: full pipeline on a sorted + indexed DAF-seq BAM | `fiberhmm-call --mode daf --enzyme ddda --region-parallel` |
| Want FIRE element calls afterwards | Pipe `fiberhmm-call -o -` into `ft fire - final.bam` |
| DddB samples | swap `--enzyme ddda` for `--enzyme dddb` in any of the above |

For Hia5 fiber-seq usage and the full CLI surface (training new models, exporting posteriors, model inspection), see the FiberHMM README.

## Further reading

- [FiberHMM repository and README](https://github.com/fiberseq/FiberHMM)
- [Molecular-annotation spec](https://github.com/fiberseq/Molecular-annotation-spec) for the `MA`/`AQ` tag schema
- [fibertools-rs](https://github.com/fiberseq/fibertools-rs) for downstream FIRE scoring and extraction
