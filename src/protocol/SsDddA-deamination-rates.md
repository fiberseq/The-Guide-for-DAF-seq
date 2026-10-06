# SsDddA activity by protein preparation

Following a 10-minute incubation with SsDddA, reactions containing two different lots of the Stergachis lab SsDddA were stopped using Stergachis lab SsDddI, whereas reactions containing EpiCypher SsDddA were stopped using EpiCypher SsDddI. All subsequent steps were performed according to the standard Targeted DAF-seq protocol.

## Targeted DAF-seq median deamination rates by SsDddA production batch


### CA10 amplicons (hg38, chr17:51829518-51834396)

| Preparation | 1 uM | 2 uM | 4 uM|
|---|---|---|---|
| Stergachis batch1 | 16% | 23% | 30% |
| Stergachis batch2 | 15% | 21% | 30% |
| EpiCypher batch | 14% | 20% | 26% |


### NAPA amplicons (hg38, chr19:47,514,488-47,518,985)

| Preparation | 1 uM | 2 uM | 4 uM|
|---|---|---|---|
| Stergachis batch1 | 32% | 40% | 47% |
| Stergachis batch2 | 32% | 38% | 46% |
| EpiCypher batch | 29% | 36% | 42% |


## PCR primers and reaction conditions

### _CA10_ region (hg38, chr17:51829518-51834396)

**Primers**  
Forward: AAGGAGTCATGAGGGACGTATGCAA  
Reverse: AGGCAGGTCCATGAAGAGTGTCCATT  
Amplicon length: 4878 bp

**PCR mix**  
SsDddA-treated DNA(~30-50ng)  
1.5 μL 5 μM Forward primer  
1.5 μL 5 μM Reverse primer  
25 μl. repliQa HiFi ToughMix(2X) (Qunatabio; Part No:95200-100)  
Water to 50 μl

**Thermocycling protocol**
1. 98 C, 30s
2. 98 C, 10s  
3. 66 C, 5s  
4. 68 C, 25s  
4. Go to step 2, 29x for 30 cycles total  
5. 68 C, 1 min
6. hold at 4 C


### _NAPA_ region (hg38, chr19:47,514,488-47,518,985)

**Primers**  
Forward: TCCCCTCCAARRCTTCAR  
Reverse: CAACCCCCRCAACCTATCA  
Amplicon length: 4498 bp

**PCR mix**  
SsDddA-treated DNA(~30-50ng)  
3 μL 5 μM Forward primer  
3 μL 5 μM Reverse primer  
25 μl. repliQa HiFi ToughMix(2X) (Qunatabio; Part No:95200-100)  
Water to 50 μl

**Thermocycling protocol**
1. 98 C, 30s
2. 98 C, 10s  
3. 56 C, 5s  
4. 68 C, 25s  
4. Go to step 2, 29x for 30 cycles total  
5. 68 C, 1 min
6. hold at 4 C

