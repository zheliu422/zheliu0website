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
