---
layout: post
title:  KAPA library prep
date:  2016-06-01
---

Preparing ezRAD libraries using the KAPA Biosystems Hyper Prep kit. The full protocol from KAPA Biosystems can be found [here](https://www.kapabiosystems.com/document/kapa-hyper-prep-kit-tds/?dl=1).

### End repair and A-tailing
Combine the following for each sample in PCR tubes:

| reagent | volume (µL) |
| ------- | ----------- |
| End repair and A-tailing buffer | 3.5 |
| End repair and A-tailing enzyme mix | 1.5 |
| DNA (digested and bead-cleaned) | 25 |
| **Total:** | **30** |

Mix and spin down briefly, then run on thermocycler:

* 30 min @ 20°C
* 30 min @ 65°C
* Hold @ 4°C

*in @ 08:42, out @ 09:42*

***

### Adapter ligation

Combine the following in PCR tubes (same tubes that A-tailing was performed in):

| reagent | volume (µL) | MasterMix for 3 rxns (x3.1) |
| ------- | ----------- | --------------------------- |
| H<sub>2</sub>O  | 2.5 | 7.75 |
| Ligation buffer | 15  | 46.5 |
| DNA Ligase      |   5 | 15.5 |
| Adapter (15 µM) | 2.5 | -- |
| DNA (post A-tailing) | 30 | -- |
| **Total:**      | **55**  | 22.5 to each tube |

Add 22.5 µL of water/buffer/ligase mastermix to each tube, then add 2.5 µL of each adapter. *Adapters graciously donated by Ingrid from the ToBo lab, from Illumina kit at 15 µM concentration.*

| library | adapter ID | adapter sequence |
| ------- | ---------- | ---------------- |
| BC      | 16         | CCGTCC(C)        |
| NC      | 18         | GTCCGC(A)        |
| ND      | 19         | GTGAAA(C)        |

Mix and spin down briefly, then run on thermocycler:

* 15 min @ 20°C
* Hold @ 4°C

*in @ 09:55, out @ 10:10*

***

### Post-ligation bead clean

Bead clean with 0.8:1 vol. beads:DNA.

1. Add 44 µL Ampure XP beads to 55 µL digested DNA (0.8:1 vol. beads:DNA)
2. Incubate at room temperature for 5 min.
3. Place on magnetic stand for 5 min.
4. Remove supernatant into waste container, leaving ~5 µL behing
5. Add 200 µL freshly made 80% ethanol (on magnetic stand)
6. Incubate 30 sec. then remove supernatant to waste container
7. Add 200 µL feshly made 80% ethanol (on magnetic stand)
8. Incubate 30 sec. then remove supernatant to waste container
9. Remove any residual ethanol using pipet
10. Let dry for 5 min., not longer than 10 min.
11. Resuspend beads in 27 µL H<sub>2</sub>O, pipet up and down
12. Incubate at room temperature for 5 min.
13. Place on magnetic stand for 5 min.
14. Transfer 25 µL supernatant to destination tube

***

### Size selection (for ~350-700bp insert)

This is a dual-SPRI bead selection, i.e., removing fragments at both the high and low ends of the distribution. The specific volumes used here represent a "0.7x - 0.5x" (left-side to right-side selection) to select for fragments between ~350 and 700bp.

1. Add 12.5 µL SPRIselect beads to 25 µL DNA (0.5:1 vol. beads:DNA)
    + This is the "right-side" selection. Fragments >~700bp bind to beads.
2. Incubate at room temperature for 5 min.
3. Place on magnetic stand for 5 min.
4. Transfer 35 µL supernatant to new tube
    + This contains fragments < 700bp, the ones we want to keep.
5. Add 5 µL SPRIselect beads to kept supernatant.
    + This is the "left-side" selection, and the bead solution:DNA volume ratio is now 0.7:1 because supernatant was already at 0.5:1, and this adds 0.2x vols more bead solution relative to original DNA volume.
6. Incubate at room temperature for 5 min.
7. Place on magnetic stand for 5 min.
8. Remove supernatant into waste container, leaving ~5 µL behing
9. Add 200 µL freshly made 80% ethanol (on magnetic stand)
10. Incubate 30 sec. then remove supernatant to waste container
11. Add 200 µL feshly made 80% ethanol (on magnetic stand)
12. Incubate 30 sec. then remove supernatant to waste container
13. Remove any residual ethanol using pipet
14. Let dry for 5 min., not longer than 10 min.
15. Resuspend beads in 13 µL **10 mM Tris-HCl**, pipet up and down
16. Incubate at room temperature for 5 min.
17. Place on magnetic stand for 5 min.
18. Transfer 11 µL supernatant to destination tube

***

### Nanodrop libraries

| library | [DNA] (ng/µL) | 260:280 | 260:230 |
| ------- | ------------- | ------- | ------- |
| BC | 4.4 | 1.96 | 9.94 |
| NC | 6.8 | 2.00 | 4.56 |
| ND | 5.6 | 1.57 | 2.74 |

Remaining 10 µL given to Amy Eggers at HIMB Core Lab for library validation (BioAnalyzer and qPCR) and sequencing.
    


