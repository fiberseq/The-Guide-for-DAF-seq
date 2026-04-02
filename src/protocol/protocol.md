# DAF-seq Protocol

This protocol covers the complete DAF-seq workflow from nuclei isolation through DNA extraction. For primer design guidelines, see [Primer Design](primer-design.md). For SsDddA and DddI purification, see [Protein Purification](protein-purification.md). After library preparation and sequencing, use the [DAF-QC Pipeline](../drylab/daf-qc.md) for data processing and quality control.

## Reagents & Buffers

### Buffer A

| Final Concentration       | Stock Concentration   | Volume stock soln |
|---------------------------|-----------------------|-------------------|
| RNase- DNase- free H2O   | 100%                  | 959 uL            |
| 15 mM Tris-Cl, pH 8.0    | 1 M Tris-Cl, pH 8.0  | 15 uL             |
| 15 mM NaCl               | 5 M NaCl              | 3 uL              |
| 60 mM KCl                | 3 M KCl               | 20 uL             |
| 1 mM EDTA, pH 8.0        | 0.5 M EDTA, pH 8.0   | 2 uL              |
| 0.5 mM EGTA, pH 8.0      | 0.5 M EGTA, pH 8.0   | 1 uL              |
| 0.5 mM Spermidine        | 0.5 M Spermidine      | 1 uL              |
| 10 nM ZnCl2              | 10 uM ZnCl2          | 1 uL              |

> **Note:** Buffer A without spermidine or ZnCl2 can be prepared in large quantities (e.g. 100 mL) and safely stored for up to 6 months at room temperature. Add 1 uL of 0.5 M spermidine and 1 uL of 10 uM ZnCl2 to 998 uL of buffer A stock right before using. Store spermidine at -20 C for up to 6 months.

### Lysis buffer
*To be optimized by user. Below are examples that have been used successfully in our lab*

#### Cell lines: 2X Lysis buffer

| Cell Line       | Final % IGEPAL   | 2X Stock solution | µl 10% IGEPAL/1ml Buffer A |
|-----------------|------------------|-------------------|----------------------------|
| K562 cells    | 0.025    | 0.05    | 5 µl    |
| HepG2    | 0.025    | 0.05    | 5 µl    |
| Lymphoblasts    | 0.025    | 0.05    | 5 µl    |
| HeLa    | 0.05    | 0.1    | 10 µl    |
| Fibroblasts| 0.1    | 0.2    | 20 µl    |      

#### Tissue: Homogenization buffer

| Final Concentration | Stock Concentration | Volume stock soln |
|---------------------|---------------------|-------------------|
| RNase- DNase- free H2O | 100% | 716 µL |
| 250mM Sucrose | 1.5M Sucrose | 167 µL |
| 15 mM Tris-Cl, pH 8.0 | 1 M Tris-Cl, pH 8.0 | 15 µL |
| 15 mM NaCl | 5 M NaCl | 3 µL |
| 60 mM KCl | 2 M KCl | 30 µL |
| 1 mM EDTA, pH 8.0 | 0.5 M EDTA, pH 8.0 | 2 µL |
| 0.5 mM EGTA, pH 8.0 | 0.5 M EGTA, pH 8.0 | 1 µL |
| 0.5 mM Spermidine | 0.5 M Spermidine | 1 µL |
| 0.1 mM DTT | 100mM DTT | 10 µL |
| 0.1% Triton X-100 | 10% Triton X-100 | 30 µL |
| 1x Protease inhibitor | 50x in EtOH (Promega G6521) | 20 µL |
| 0.2U RNasein plus | 40U/ul RNasein plus | 5 µL |

> **Note:** Nuclei isolation is cell and tissue-type dependent and should be optimized by the user to ensure completion. Digitonin is also compatible.

### Additional reagents

- 1x PBS, pH 7.4 + 0.5% BSA (for cells)
- UNG inhibitor (NEB M0281)
- SsDddA stock*: 100 uM, aliquots stored at -80 C
- DddI stock*: 1000 uM, aliquots stored at -80 C
- NEB Monarch Spin gDNA Extraction Kit (T3010)
- Qubit dsDNA assay
- LoBind tubes

&#42; See [Protein Purification](protein-purification.md) for how to generate these. You can also e-mail absterga@uw.edu for protein aliquots

---

## Nuclei Isolation

### Example for cells
*Below is an example protocol which we have used for LCLs. Nuclei isolation should be optimized by the user for each tissue and cell type.*

1. Collect 250k-1M cells into a 1.5 mL LoBind tube.
2. Pellet at 350 x g for 5 min at 4 C. Remove supernatant.
3. Wash cells with 1 mL 1x PBS, pH 7.4 + 0.5% BSA.
4. Pellet at 350 x g for 5 min at 4 C. Remove supernatant.
5. Resuspend pellet in 60 uL Buffer A.
6. Add 60 uL 2x Lysis Buffer (1:1 dilution to a final 1× Lysis Buffer concentration). Mix by gently tapping the side of the tube and incubate 10 min on ice.
7. Spin 350 x g for 5 min at 4 C. Remove supernatant.
8. Resuspend nuclei in 50 uL Buffer A.

<div class="warning">

**IMPORTANT:** Ensure that cells are fully lysed before proceeding to the next step.

</div>

9. Count 100k-250k nuclei and add Buffer A + 1 uL UNG inhibitor (2 U) to a final volume of 47 uL.
10. Continue to [On-Nuclei Cytidine Deamination](protocol.md#on-nuclei-cytidine-deamination)

### Example for tissues
*Below is an example protocol which we have used for tissues including liver and brain. Nuclei isolation should be optimized by the user for each tissue and cell type. Some tissues such as muscle may require pulverization with LN2 in a mortar prior to douncing*

1. Add 1mL homogenization buffer and tissue to dounce, keep on ice.
2. Homogenize the tissue with:
   * 10 strokes of the loose pestle A (avoid adding too much pressure and avoid foaming)
   * 10 strokes of the tight pestle B (avoid adding too much pressure and avoid foaming)
3. Using a wide bore P1000 pipette tip, transfer homogenate out of the dounce and pass it through a 70µm cell strainer into a 15 ml low bind tube.
4. Centrifuge 350xg for 5 min at 4°C.
5. Discard supernatant. Keep pellet.
6. Resuspend nuclei in 50 µL cold buffer A. Mix gently and count nuclei.

<div class="warning">
  
**IMPORTANT:** Ensure that cells are fully lysed before proceeding to the next step

</div>

7. Count 100k-250k nuclei and add Buffer A + 1 µL UNG inhibitor (2 U) to a final volume of 47 µL.
8. Continue to [On-Nuclei Cytidine Deamination](protocol.md#on-nuclei-cytidine-deamination)

---

## On-Nuclei Cytidine Deamination

1. Add 2 µL SsDddA (100 µM stock, final 4 µM) to the 47 µL nuclei suspension.
2. Incubate 10 min at 25°C in a PCR machine or heat block. Mix gently; avoid vortexing.
3. Immediately add 1 µL DddI (1000 µM, 5-molar excess) to stop the reaction. Mix by gently tapping.
4. Proceed according to your application:

    a. **Targeted DAF-seq:** Proceed to [DNA Extraction for Targeted DAF-seq](protocol.md#dna-extraction-for-targeted-daf-seq). Deaminase reactions may be safely stored at -20°C.
    
    b. **Single-cell DAF-seq:** Proceed to [Single-cell DAF-seq Fluorescence-Activated Cell Sorting (FACS)](protocol.md#single-cell-daf-seq-fluorescence-activated-cell-sorting-facs). Maintain nuclei on ice until sorting.

---

## DNA Extraction for Targeted DAF-seq

*Follow the manufacturer's instructions. The steps below reflect the lab's working sequence for samples after the on-nuclei deamination stop. For routine targeted DAF-seq applications, we recommend NEB Monarch Spin gDNA Extraction Kit (T3010) as the length of isolated DNA is typically sufficient for the amplification of 2-7 kb products. A HMW kit may be necessary for longer range PCR products.*

1. Add PBS to bring the total volume to 100 uL (typically 50 uL).
2. Add 1 uL Proteinase K and 3 uL RNase A; mix by brief vortexing.
3. Add 100 uL Cell Lysis Buffer; vortex 10 s.
4. Incubate 5 min at 56 C in a thermal mixer with agitation (~1400 rpm).
5. Add 400 uL gDNA Binding Buffer; vortex 5-10 s.
6. Centrifuge briefly (~1 min at 16,000 x g) if needed to collect contents; transfer to a gDNA purification column seated in a collection tube.
7. Close cap and centrifuge 3 min at 1,000 x g to load/bind DNA onto the column.
8. Immediately centrifuge 1 min at 16,000 x g to clear the membrane.
9. Discard collection tube and place column into a fresh collection tube.
10. Add 500 uL gDNA Wash Buffer; centrifuge 1 min at >=12,000 x g.
11. Discard flow-through and repeat the 500 uL Wash Buffer step and spin.
12. Transfer column to a clean 1.5 mL LoBind tube.
13. Add 35 uL pre-warmed (56 C) gDNA Elution Buffer directly to the membrane.
14. Let stand 1 min at room temperature; centrifuge 1 min at >=12,000 x g to elute DNA.
15. Store eluted gDNA at 4 C (short-term) or -20 C (long-term). Quantify with Qubit.

**The DNA is now ready for PCR.**

---

## Single-cell DAF-seq Fluorescence-Activated Cell Sorting (FACS)

1. Aliquot 3 ul of BioSkryb Cell Buffer into desired wells of a 96-well PCR plate. Leave first or last column empty to allow space for BioSkryb PTA controls.
2. Create forward scatter (FSC-A & FSC-H) and side scatter (SSC-A) gates to remove doublets and debris.
3. Sort individual nuclei into plate wells containing BioSkryb Cell Buffer.
4. Seal and quickly centrifuge the nuclei plate.
5. Flash freeze the nuclei plate at -80C or dry ice and store until PTA amplification.

---


## Notes

- The reaction volume of the "On-Nuclei Cytidine Deamination" may be doubled to accommodate 500K nuclei in step 9. If 100 uL volume is used, no additional buffer is required at step 14 of "DNA Extraction".
- We have observed that the recovery of SsDddA-treated DNA is approximately 10-20% as efficient as untreated DNA using the Monarch Spin gDNA Extraction Kit. This recovery is typically sufficient for downstream applications.
- Buffer A is compatible with SsDddA provided by our lab. Other cytidine deaminases may require buffers containing ZnCl2.

---

## Next steps

After library preparation and sequencing, process your data with the [DAF-QC Pipeline](../drylab/daf-qc.md) to assess targeting efficiency, deamination rates, strand calling, and other quality metrics.
