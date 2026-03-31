# Primer Design

A strategy for designing primers for targeted DAF-seq experiments.

## Materials

- **Untreated gDNA:** We recommend a median size of ~20 kb for most applications, which we routinely isolate using the Monarch Spin gDNA Extraction Kit (T3010).
- **DAF-seq DNA:** SsDddA-treated chromatin followed by DNA extraction (see [DAF-seq Protocol](protocol.md)). For primer validation, chromatin from a readily available/cheap source that contains the target locus of interest should be used (e.g. cell lines), although the target sample is preferred when possible.
- **Uracil-tolerant DNA polymerase/PCR master mix:** It is critical to use a DNA polymerase that tolerates uracil in the template. We have had the best results with RepliQa HiFi ToughMix (QuantaBio, 95200). Other uracil-tolerant polymerases we have tested with varying results include Q5U (NEB M0597), PhusionU (Thermo Scientific F562), LongAmp (NEB M0323), and KOD One (Toyobo KMM-101).
- **PCR cleanup kit:** We use Monarch Spin PCR & DNA Cleanup Kit (NEB T1130), but most kits should work as long as they can process the proper PCR fragment size.

---

## Identify a target window

Targeted DAF-seq is typically performed to amplify 2-10 kb targets using PCR (see [Choosing a product length](#choosing-a-product-length) below). We recommend that primer binding sites are designed to be at least 100 bp outside of the genomic element of interest (preferably >500 bp). Below are features to consider when designing primers (in order of priority):

1. When possible, keep multiple regulatory elements within the same amplicon if co-actuation is to be considered as part of the analysis.
2. Avoid placing primer binding sites directly within accessible chromatin regulatory elements within your sample of interest, which can typically be determined using existing orthogonal datasets such as ATAC-seq, DNase-seq, or Fiber-seq.
3. Avoid placing primer binding sites within repetitive elements, which can be identified using the RepeatMasker track in the UCSC genome browser.
4. Avoid placing primer binding sites directly over common germline genetic variants within your species of interest. If you are using human samples for which a germline VCF is not available, avoid common variants, which can be displayed in the UCSC browser gnomAD track (be sure to select "All" annotation types; we recommend a threshold of 0.01).
5. Consider avoiding primer binding sites that result in internal repetitive elements with multiple copies within the amplified region. In some cases, homologous repeats can cause deletions within PCR products. This is easily detected by shallow sequencing and should not be prioritized in the first round of design if it compromises inclusion of desired elements.

---

## Design candidate primers

Primer design for DAF-seq requires unique considerations due to template deamination. The guidelines below represent a primer design strategy using NCBI primer-BLAST followed by curation.

As each region and deamination pattern is unique, it may not always be possible to satisfy all recommendations:

1. **Set design parameters:** Paste the target region and specify the positions in which to design primers. Set the PCR product size to the desired range. You may also broaden the "Primer melting temperatures" if few primers are returned.

    In the "Primer Pair Specificity Checking Parameters", change "Database" to "Refseq representative genomes", and increase the "Max target amplicon size" as appropriate (typically a few kb higher than the intended target).

    In "Advanced parameters", change "Primer Size" to 20-28 (optimal 23). Change "Primer GC content(%)" to 20-50%. Change "Max Poly-X" to 3 (see [Poly-X stretches](#poly-x-stretches)). Change "Max GC in primer 3' end" to 3.

2. **Curate primers for the following:**
    1. **Specificity (critical):** For primers with identified off-target sites, pay special attention to those where a C>T mutation would make a better primer binding site. Reject primer candidates with many partial off-target matches.
    2. **C/G in 3' end (critical):** Prefer primers with the absence of C/G in the terminal 3 bases on the 3' end, although primers with the absence of C/G in the terminal 2 bases have also been successful for DAF-seq.
    3. **Minimize C/G content (preferred):** When possible, prefer primers with <40% C/G.
    4. **Balance C/G (optional):** See [C and G in primers](#c-and-g-in-primers).

3. **Select primer sets for testing:** From our experience, less than 50% of selected primer sets will successfully amplify a single band with SsDddA-treated template. For this reason, we recommend selecting several primer sets per target to accelerate screening.

---

## PCR annealing temperature gradient with gDNA

<div class="warning">

**Critical:** Ensure that the DNA polymerase tolerates uracil in the template. We have had the best results with RepliQa HiFi ToughMix (QuantaBio, 95200). Other uracil-tolerant polymerases include Q5U, PhusionU, LongAmp, and KOD One.

</div>

Perform an annealing temperature gradient on primer candidates using untreated gDNA template. We prefer to use gDNA for validation at this point both because gDNA is cheaper and easier to produce and because primer binding sites are intentionally designed outside of known regulatory elements, so the majority of the final DAF-seq template should be nucleosome-protected and unmodified, as is simulated by gDNA. Basically, if it doesn't work on gDNA, it won't work for DAF-seq.

Look for primer sets that produce a single band of the anticipated size in agarose gel electrophoresis. Low off-target amplification may be tolerable if primer choices are limited. If multiple temperatures produce comparable amplification of the single product, we prefer the lowest temperature which should theoretically have more tolerance for deaminations in DAF-seq DNA.

If multiple primer sets are successful at this stage, we recommend comparing the performance of all of them through sequencing on DAF-seq template.

---

## Validate PCR with DAF-seq template and shallow sequencing

Perform PCR amplification on DAF-seq template with the best primer sets and annealing temperatures determined in the previous step. We recommend a 50 uL reaction. Run ~10 uL on an agarose gel to validate the presence of a single band. Off-target amplification may be tolerable if primer choices are limited.

Purify the remaining product with a PCR cleanup kit. We do not recommend gel extraction as the buffers can interfere with subsequent sequencing.

Perform shallow sequencing with a long-read method. We typically use the ONT-based Plasmidsaurus Premium PCR (standard) for routine validation. In our experience, primers that perform well in shallow ONT-based sequencing have also performed well on full-scale PacBio sequencing.

---

## Run QC to evaluate primer performance

Run the [DAF-QC-SMK pipeline](../drylab/daf-qc.md) to evaluate primer performance. Optimal primers will have:

- Low (<10%) off-target amplification
- A high proportion of full-length reads (>80%)
- Approximately 50/50 ratio of CT/GA reads, although primer sets with substantial strand bias may be acceptable for some applications (such as when identifying single nucleotide variants is not critical)

Also be sure to visualize reads in IGV. Check for any internal deletions and evaluate whether they are haplotype-specific. Non-haplotype-specific deletions may represent PCR artifacts that can be resolved by tuning PCR conditions or redesigning primer binding sites to exclude problematic repetitive regions (see point 5 in [Identify a target window](#identify-a-target-window)).

---

## Additional considerations

### Primer design rules are not rigid

Primer design for DAF-seq can be much more difficult than typical PCR primer design. Identifying primer sets with high specificity is challenged by the presence of template modifications and the preference to minimize C/G content. For the most difficult targets, a flexible approach that bypasses some of the recommendations above may be necessary.

### Nucleosome protection is an asset

When a regulatory landscape is known through alternative datasets, it is important to avoid primer binding sites overlapping accessible elements. With this in mind, most of the template DNA will be nucleosome-occluded as nucleosome footprints are ~147 bp, while internucleosomal linker regions (i.e. accessible regions between nucleosomes that are not regulatory elements) are closer to ~10 bp. This means that most template strands will be complementary to primers even within C/G positions.

### Degenerate bases in primers

To account for the possibility that there could be deaminations within primer binding sites, our initial publication used primers designed with degeneracy at G genomic positions in the form of randomly incorporated G or A (IDT). Given the point above regarding nucleosome protection, we later reconsidered this design and tested whether degenerate bases facilitate amplification. In general, we found that targets amplified better without degenerate bases.

### Selection of PCR polymerase

It is critical to select a polymerase tolerant of uracil in the DNA template. This is one of the most common mistakes. Polymerase fidelity will also impact the quality of results, especially if deduplication is desired as spurious mutations can cause duplicates to be missed. The polymerase must also be suitable for relatively long-range amplifications, although this is quite common. We have found that RepliQa HiFi ToughMix (QuantaBio, 95200) fulfills these requirements and has been relatively robust in our hands.

### Locked nucleic acids (LNAs) for difficult targets

In specialized cases, we have used primer sets containing locked nucleic acids to boost product yield and annealing temperature (e.g. when needed for compatibility in multiplexed assays or for C/G-rich templates prone to forming secondary structures). We have found that primers containing a single LNA are tolerated in PacBio and ONT sequencing, but adding more than one LNA causes substantial sequencing dropout with PacBio (ONT not tested). As LNA-containing primers are substantially more expensive, we recommend adding them only when a faint on-target band is already observed and multiple primer sets have failed.

In our hands, we have observed improved yield with LNAs positioned within 5 bases of the 3' and 5' ends, and we typically add them between A/A, A/T, or T/T bases. The effects of LNAs on primer specificity are complex, and LNA-containing primers have only been superficially explored in our lab. We recommend further literature review for users requiring LNA-containing primers.

### Multiplexed assays

We have successfully designed primer sets for multiplexed PCR, although this can be extremely challenging. Try to design primers with comparable predicted annealing temperatures and then test empirically using a PCR annealing temperature gradient with gDNA template. LNAs can be used to boost primer annealing temperatures if needed.

Once compatible annealing temperatures have been established, try the multiplex PCR using an equimolar ratio of primers, purify the product, and sequence with shallow long-read sequencing (i.e. Plasmidsaurus Premium PCR sequencing or similar). Check that the sequencing yield of each target is as desired (typically equal, but you may wish to prioritize a specific amplicon for some applications). Tune primer ratios by titration if needed, and reconfirm with sequencing.

### Choosing a product length

Target amplicon length is typically 2-10 kb. The lower limit is set to include multiple nucleosome-bound stretches which are important for genomic alignment, and we do not recommend smaller for most applications. The upper limit is more flexible, but constrained by the same challenges as conventional long-range PCR. However, primer specificity can be even more critical because deamination events within the template can create stronger off-target binding sites.

### Poly-X stretches

*Details on poly-X stretch considerations are being finalized.*

### C and G in primers

A matter of ongoing discussion is whether to preferentially avoid G bases only or both G and C bases in primer design. SsDddA converts cytosine to uracil bases, so G bases in the primers have the potential for mismatch upon the first PCR cycle. However, on the second cycle, SsDddA-converted uracil bases that were on the 3' end of the PCR-synthesized strand are now A bases at positions complementary to C within the primer. Some lab members have prioritized the first round of amplification by preferentially excluding G. Others argue that an equal C/G ratio in primers is important to maximize efficient amplification on both the first and second cycles, which is important for exponential amplification and anecdotally reduces biases for top vs bottom strands. In practice, the exact choice may not be critical as the majority of DAF-seq template is anticipated to be nucleosome-protected and unmodified at primer binding locations, and DAF-seq primers have been successfully designed with both strategies.

---

## Feedback

DAF-seq is an emergent technology, and we are still improving our primer design methodology. If you have suggestions or collaboration ideas for making this process more robust, please reach out.
