---
title: 1-Bit SRAM Cell in 45-nm CMOS Technology with Integrated Dynamic Power Supply
subtitle: 

# Summary for listings and search engines
summary: Dynamic Cell Vcc proves the improvement in both Read and Write margins and leakage saving

# Link this post with a project
projects:

# Date published
date: "2022-01-10T00:00:00Z"

# Date updated
lastmod: "2022-02-12T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
# image:
  # caption: 'Image credit: [**predictabledesigns.com**](https://predictabledesigns.com/introduction-to-analog-to-digital-converters-adc/)'
  # focal_point: ""
  # placement: 2
  # preview_only: false

authors:
- admin

tags:
- Academic
- Class Project

categories:
- SRAM
- Validation
---

## Overview
The design exhibits a 4 GHz 1-bit SRAM cell on 45nm CMOS technology. A based dynamic power supply is integrated into the design with a motivation to switch between two voltage levels (Vcc_hi and Vcc_lo) during READ and WRITE operations. This design has been implemented in Cadence Virtuoso for both schematic as well as the layout. The simulation result has proven the improvement in both Read and Write margins. Furthermore, simulation showed the SRAM cell leakage power consumption is reduced.

## PROBLEM CONTEXT
One of the main focuses of small-scale SRAM design is to achieve a balanced cell stability with optimized device sizing. However, there are a few challenges that need to be faced. One of these challenges is growing threshold voltage variations due to random dopant fluctuations. This can raise the sensitivity of status noise margin (SNM) to these process variations. Additionally, a mismatch in threshold voltage can lead to a mismatch in current on both halves of an SRAM cell. Generally, we want to prevent degradation of SNM, and we want the current on both halves to be identical. But we cannot dynamically change the threshold voltage of the sizing of these transistors. 
Power dissipation in SRAM circuits can be categorized into two main types - dynamic and static power dissipation. For static power dissipation, it is due to leakage current drawn from the power line. The main contributor of leakage current is the sub-threshold current. For SRAM, during idle phase, the workline (WL) is at WL=0 and two bitlines are precharged to BL=1, BLB=1. Thus there are two major leakage paths, 1)  Cell Vcc to ground and 2) BL (BLB) to ground through the access transistor. Generally, the static power dissipation can be expressed as equation:
Pstatict =Vdd*Isub*e(Vgs -Vt)/nVth
We can see the exponential increase of subthreshold leakage drain current with decreasing Vt for a given Vgs. This further proves that changing threshold voltage may lead to more negative impact on SRAM operation. In section II, we will discuss our proposed design and what this contributes to cell margins, stability, and leakage. 

## STATE OF THE ART & CONTRIBUTION
We propose dynamically switching between two voltage levels during read and write operations. In doing so, we can improve read and write margins independently without compromising each other. During write mode, we apply a supply voltage lower than the Word Line (WL) voltage. This weakens the pull-up network of the cell. During a read operation, we apply a supply voltage larger than the WL voltage. This strengthens the pull-down network which reduces read voltage and increases the trip point. Earlier research [1] has shown how margins can be improved using a dynamic power supply voltage. But they exclude Monte Carlo methodologies to find a relationship between supply voltage and average access delay. In this paper, we plan to confirm their key discoveries in margins and leakage power saving by conducting a waveform analysis on an SRAM schematic. Then, we propose designing an SRAM cell layout and conducting a Monte Carlo simulation to model a gaussian distribution of average access time. We then estimate read and write failures based on this distribution. The goal of this design is to improve margins, reduce access delay, and increase leakage power saving.

## METHODOLOGY
First, a schematic of an SRAM was created. Pfets were sized to 90 nm. Access transistors were sized to 135 nm. Nfets were sized to 180 nm. This cell was used for waveform analysis to measure the margins. To measure the write margin, The bit line (BL) voltage was sweeped to estimate the minimum voltage needed to create a transition at the storage node. To measure the read margin, we needed to find the difference between the trip point and the read voltage. 
We then implemented a layout for one SRAM cell because layout will help us understand the intricate details of parasites. Also, a Monte Carlo simulation could be done on the layout to help us study the Rise and Fall delay improvement of our proposed method. The SRAM cell layout followed a classical design approach. The cell has a length of 1.67nm and width of 1.93nm. After DRC and LVS checks, a netlist is created using PEX tools. The netlist is for the use of HSpice to help us with Monte Carlo analysis. We applied ΔVt = 0.08V with 5 nm change in Wp, Lp, and Ln, 10 nm change in Wn. For the delay analysis, the fall delay is defined as the time that data fall from 95% to 5% of Vcc. For rise delay, it is defined as the time that data rises from 5% to 95% of Vcc.

## KEY FINDINGS
Using a standard 1.0V supply voltage, the write margin was measured to be 397mV. With a 800mV supply voltage, the write margin was measured to be 481mV. So, the write margin increased when we apply Vcc_Low. Two waveforms can be seen below that illustrate the waveform for this transient analysis.
{{< figure src="key_find1.jpg" title="Write margin for baseline" >}}
{{< figure src="key_find2.jpg" title="Write margin for proposed dual Vcc design" >}}
Next, the read margins were measured. The switching threshold was measured to be 415mV using a DC sweep. Then, both BLs were precharged to 1.0V. When WL high, the voltage at the storage node was measured under both scenarios - this is the read voltage. The read margin is the difference between the trip point and the read voltage. With standard supply voltage, the read margin was estimated to be 271mv. With Vcc_Hi, it was estimated to be 285mV. So the read margin was measured to be higher with Vcc_High.
{{< figure src="key_find3.jpg" title="Read margin for baseline" >}}
{{< figure src="key_find4.jpg" title="Read margin for proposed dual Vcc design" >}}
To perform the statistical analysis of the SRAM cell, a Monte Carlo simulation of 800 samples has been carried out. Fig. 3 below is the Monte Carlo simulation result for writing a “1” on Q.
{{< figure src="monte.jpg" title="Baseline Monte Carlo simulation result for writing “1”" >}}
The rise and fall delay were measured for both baseline and our proposed dual Vcc method. For fall delay, the average fall delay for our method decreased to 252.26 ps compared to average fall delay of 329.46 ps for baseline. However, the proposed dual Vcc method shows a degraded rise delay. The baseline has an average rise delay of 115.82 ps while our method has an average rise delay of 127.4 ps. This is one trade-off for using lower Vcc. In a MOSFET, the higher the difference between the gate and source voltages, the higher the current that transistor will pass. The driving voltages on the gates are reduced when Vcc is reduced, as is the amount of current they pass. Because SRAM loads are mostly capacitive, the amount of current that is delivered directly affects the rate at which that node’s voltage changes. Hence, the rise delay is larger.
{{< figure src="monte_1.jpg" title="Monte Carlo distribution for fall delay">}}
{{< figure src="monte_2.jpg" title="Monte Carlo distribution for rise delay">}}
A leakage analysis has been performed on one SRAM cell. The reported leakage current at t=1.59 ns for baseline 1V Vcc is 8.84 nA. As for our proposed dual Vcc operation, the standby voltage for cell supply is 0.8V. At same time stamps, the leakage current is 3.037 nA. Compare the result, our dual Vcc method saved around 72.52% of leakage power during idle phase. We then performed a parametric analysis and sweeped cell Vcc from 0.8V to 1.2V. As the result shows in the figure below. The leakage saving is maximized at Vcc = 0.8V.  
{{< figure src="leak.jpg" title="Vcc vs. Leakage current in idle phase">}}
Below is a summary of our analysis. With our proposed design, we achieved a higher read and write margin. Furthermore, we achieved a lower average fall delay, but not a faster rise time. One solution could be raising the supply voltage when the storage nodes meet to help with amplification. That way the P-FETs are stronger. All in all, we can generally improve write operations, while minimizing negative impacts in rise delay, which makes this an effective design.
  | Item   | Write Margin | Read Margin | Monte Carlo Average Fall Delay | Monte Carlo Average Rise Delay |
  | ------------- | ------------- |------------- | ------------- |------------- |
  | Baseline   | 397.8 mV	| 271 mV | 329.46 ps |	115.82 ps |
  | Dynamic Vcc  | 481.7 mV |	285 mV |	252.26 ps|	127.4 ps |
  
## FUTURE WORK
In the future, we plan to expand our work from one cell to one bank (2kB). Our hope would be to integrate column-based power supply techniques to further improve cell stability. That way, we can test our functionality under a more complex scheme. In addition, we could further analyze leakage power saving for a more complete design.

## References
[1] K. Zhang et al., "A 3-GHz 70MB SRAM in 65nm CMOS technology with integrated column-based dynamic power supply," ISSCC. 2005 IEEE International Digest of Technical Papers. Solid-State Circuits Conference, 2005., 2005, pp. 474-611 Vol. 1, doi: 10.1109/ISSCC.2005.1494075.
[2] 6T SRAM Cell Design, https://www.iue.tuwien.ac.at/phd/entner/node34.html 
E. Grossar, M. Stucchi, K. Maex and W. Dehaene, "Read Stability and Write-Ability Analysis of SRAM Cells for Nanometer Technologies," in IEEE Journal of Solid-State Circuits, vol. 41, no. 11, pp. 2577-2588, Nov. 2006, doi: 10.1109/JSSC.2006.883344.
[3] Tripti Tripathi , Durg Singh Chauhan, Sanjay Kumar Singh, “A Novel Approach to Design SRAM Cells for Low
Leakage and Improved Stability,” Journal of Low Power Electronics and Applications
[4] M. Mamidipaka, K Khouri, N Dutt, M. Abadir, “Leakage Power Estimation in SRAMs,” CECS Technical Report #03-32
