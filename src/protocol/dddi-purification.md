# DddI Purification with FPLC Protocol

This protocol for the expression and purification of DddI was compiled and optimized by Devaraja G. Mudeppa (Stergachis Lab, Division of Medical Genetics, University of Washington).

---

## Buffers & Reagents

### Buffer A

| Component | Final Concentration |
|---|---|
| Tris-HCl, pH 7.8 | 50 mM |
| NaCl | 600 mM |
| Glycerol | 10% |
| Imidazole | 10 mM |
| Triton X-100 | 0.1% |
| 2-Mercaptoethanol | 5 mM |

### Wash Buffer

| Component | Final Concentration |
|---|---|
| Tris-HCl, pH 7.8 | 50 mM |
| NaCl | 500 mM |
| Imidazole | 30 mM |
| 2-Mercaptoethanol | 5 mM |

### Buffer B

| Component | Final Concentration |
|---|---|
| Tris-HCl, pH 8.0 | 50 mM |
| NaCl | 600 mM |
| Imidazole | 500 mM |
| Glycerol | 10% |

### Storage Buffer

| Component | Final Concentration |
|---|---|
| Tris-HCl, pH 7.8 | 50 mM |
| NaCl | 500 mM |
| DTT | 1 mM |
| Glycerol | 10% |

### Additional Reagents

* IPTG stock: 1 M in water
* Kanamycin stock: 100 mg/mL in water

---

## Equipment

* Shaker incubator
* Centrifuge capable of up to 40,000 × g
* Sonicator with a 13 mm probe
* FPLC system
* Spectrophotometer

---

## DddI Expression

1. Transform BL21(DE3) with pColDuet_nHis_SsDddI, plate on LB-kan agar (50 µg/mL). Incubate overnight at 37 °C.
2. Inoculate a single colony from the plate into 12 mL LB containing 6 µL of kanamycin stock (100 mg/mL).
3. Grow overnight at 37 °C with shaking at 250 rpm.
4. Add 10 mL of the overnight culture to 1 L of LB containing 500 µL of kanamycin stock (100 mg/mL).
5. Grow at 37 °C with shaking at 250 rpm for approximately 5 hours.
6. Measure OD600 and adjust to OD600 ≈ 0.6 if necessary, using fresh LB medium.
7. Briefly cool the culture by placing it on ice for a few minutes.
8. Add 300 µL of 1 M IPTG to 1 L of culture to achieve a final concentration of 0.3 mM.
9. Incubate at 25 °C with shaking at 250 rpm for approximately 18 hours.
10. Pellet cells (4000 × g, 10 min) and store the cell pellet at −80 °C.

---

## DddI Purification

> **Note:** All purification steps were performed at 4 °C. Unless noted, the flow rate was 2 mL/min.

1. Thaw the 1 L culture pellet at room temperature for 10 minutes (skip this step if using a fresh pellet).
2. Add 35 mL of Buffer A containing two cOmplete Mini EDTA-free protease inhibitor tablets (Millipore-Sigma; Cat# 11836170001). Vortex vigorously for 2–3 minutes.
3. Transfer the resuspended cells to a 50 mL Falcon tube and vortex again to eliminate lumps.
4. Sonicate with a 13 mm probe for a total time of 10 min (30 s on/30 s off cycles) at 30% amplitude.
5. Centrifuge the lysate at 30,000 × g for 30 min.
6. Load the supernatant onto a 5 mL HisTrap Excel column (Cytiva; Cat# 17371206), which has been pre-equilibrated with 5 column volumes (CV) of Buffer A.
7. Wash the column with 5 CV of Buffer A, then 10 CV Wash Buffer.
8. Elute column-bound DddI by applying a 5 CV (25 mL) gradient from 100% Wash Buffer to 100% Buffer B.
9. The protein eluted between ~30% and ~70% was collected.
10. Concentrate eluted DddI using a 15 mL 3 kDa MWCO Amicon filter (Millipore Sigma; Cat# UFC900308).
11. Perform buffer exchange by diluting the protein to 15 mL with Storage Buffer and reconcentrating to 1 mL; repeat this step 3 times.
12. Quantify purified DddI using the Bradford assay. Adjust DddI concentration to 1000 µM using Storage Buffer. Verify purity using 4–20% SDS-PAGE.
13. Store the purified DddI in required aliquots at −80 °C. The DddI is stable for at least 5 freeze-thaw cycles.

