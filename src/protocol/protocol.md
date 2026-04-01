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

### 2X Lysis buffer (or substitute)

| Cell Line       | Final % IGEPAL   | 2X Stock solution | µl 10% IGEPAL/1ml Buffer A |
|-----------------|------------------|-------------------|----------------------------|
| K562 cells    | 0.025    | 0.05    | 5 µl    |
| HepG2    | 0.025    | 0.05    | 5 µl    |
| Lymphoblasts    | 0.025    | 0.05    | 5 µl    |
| HeLa    | 0.05    | 0.1    | 10 µl    |
| Fibroblasts| 0.1    | 0.2    | 20 µl    |      

> **Note:** Nuclei isolation is cell and tissue-type dependent and should be optimized by the user to ensure completion. Triton or digitonin (e.g 0.1% (w/v)) can be substituted for IGEPAL.

### Additional reagents

- 1x PBS, pH 7.4 + 0.5% BSA
- UNG inhibitor (NEB M0281)
- SsDddA stock*: 100 uM, aliquots stored at -80 C
- DddI stock*: 1000 uM, aliquots stored at -80 C
- NEB Monarch Spin gDNA Extraction Kit (T3010)
- Qubit dsDNA assay
- LoBind tubes

* See [Protein Purification](protein-purification.md) for how to generate these. You can also e-mail absterga@uw.edu for protein aliquots

## Nuclei Isolation

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

---

## On-Nuclei Cytidine Deamination

10. Add 2 uL SsDddA (100 uM stock, final 4 uM) to the 47 uL nuclei suspension.
11. Incubate 10 min at 25 C in a PCR machine or heat block. Mix gently; avoid vortexing.
12. Immediately add 1 uL DddI (1000 uM, 5-molar excess) to stop the reaction. Mix by gently tapping.
13. (Optional) Store at -20 C before DNA extraction.

---

## DNA Extraction

*Follow the manufacturer's instructions. The steps below reflect the lab's working sequence for samples after the on-nuclei deamination stop. For routine targeted DAF-seq applications, we recommend NEB Monarch Spin gDNA Extraction Kit (T3010) as the length of isolated DNA is typically sufficient for the amplification of 2-7 kb products. A HMW kit may be necessary for longer range PCR products.*

14. Add PBS to bring the total volume to 100 uL (typically 50 uL).
15. Add 1 uL Proteinase K and 3 uL RNase A; mix by brief vortexing.
16. Add 100 uL Cell Lysis Buffer; vortex 10 s.
17. Incubate 5 min at 56 C in a thermal mixer with agitation (~1400 rpm).
18. Add 400 uL gDNA Binding Buffer; vortex 5-10 s.
19. Centrifuge briefly (~1 min at 16,000 x g) if needed to collect contents; transfer to a gDNA purification column seated in a collection tube.
20. Close cap and centrifuge 3 min at 1,000 x g to load/bind DNA onto the column.
21. Immediately centrifuge 1 min at 16,000 x g to clear the membrane.
22. Discard collection tube and place column into a fresh collection tube.
23. Add 500 uL gDNA Wash Buffer; centrifuge 1 min at >=12,000 x g.
24. Discard flow-through and repeat the 500 uL Wash Buffer step and spin.
25. Transfer column to a clean 1.5 mL LoBind tube.
26. Add 35 uL pre-warmed (56 C) gDNA Elution Buffer directly to the membrane.
27. Let stand 1 min at room temperature; centrifuge 1 min at >=12,000 x g to elute DNA.
28. Store eluted gDNA at 4 C (short-term) or -20 C (long-term). Quantify with Qubit.

**The DNA is now ready for PCR.**

---

## Notes

- The reaction volume of the "On-Nuclei Cytidine Deamination" may be doubled to accommodate 500K nuclei in step 9. If 100 uL volume is used, no additional buffer is required at step 14 of "DNA Extraction".
- We have observed that the recovery of SsDddA-treated DNA is approximately 10-20% as efficient as untreated DNA using the Monarch Spin gDNA Extraction Kit. This recovery is typically sufficient for downstream applications.
- Buffer A is compatible with SsDddA provided by our lab. Other cytidine deaminases may require buffers containing ZnCl2.

---

## Next steps

After library preparation and sequencing, process your data with the [DAF-QC Pipeline](../drylab/daf-qc.md) to assess targeting efficiency, deamination rates, strand calling, and other quality metrics.
