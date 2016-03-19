---
layout: post
title: DEB_photoinhibition
date: 2016-03-18
categories:
---
Modeling photoinhibition in coralDEB:
•yCL = yield of carbon from photons (=quantum efficiency)
•under normal conditions, yCL = yCLmax (=~0.05 mol fixed C/mol photons)
•excess light (eL) reduces quantum efficiency (photoinhibition) by the formula: 
yCL = yCLmax / (1 + ((eL/S) / L50)^k); 
L50 and k are constants describing the threshold and sensitivity to excess light
•reduced yCL means it takes more photons to produce equivalent amount of fixed carbon (quantum efficiency has been reduced!)
•however, these photons are not all used up in fixing carbon--rather, they need to be rejected by the photosynthesis SU and count towards eL
• excess light must be calculated as the uptake of light minus the amount of light used (quenched) in fixing carbon. The latter quantity is equal to the amount of carbon produced by the SU divided by yCLmax (**not** yCL). If the reduced yCL is used to calculate light used, this would mean that all the additional photons are being used in photosynthesis, and no excess light is generated.
•Therefore, we use yCL (which can be reduced by eL) to calculate the amount of carbon fixed, but yCLmax (which is fixed) to calculate the amount of photons actually used to fix carbon, and subsequently the amount of excess light. 

