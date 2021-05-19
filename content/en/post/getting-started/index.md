---
title: ADC design
subtitle: 

# Summary for listings and search engines
summary: This page presents a two stage fully differential pipelined SAR ADC design that I worked on during Spring 2021

# Link this post with a project
projects:

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**predictabledesigns.com**](https://predictabledesigns.com/introduction-to-analog-to-digital-converters-adc/)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- Academic

categories:
- ADC
---

## Overview

In this project, we designed a 2-stage pipelined Successive Approximation Register (SAR) Analog to Digital Converter (ADC). SAR ADC architectures are popular for achieving high energy efficiency but they suffer from resolution and speed limitations. The pipelined SAR architecture divides a moderate resolution SAR ADC into some low resolution SAR ADCs.
The target specifications are given in the following table:
  | Item   | Specifications |
  | ------------- | ------------- |
  | Technology   | 45nm (NCSU FreePDK45) |
  | Power supply  | VDD = 1.2V, VSS = 0V  |
  | Resistor size | < 100kΩ  |
  | Power supply  | VDD = 1.2V, VSS = 0V  |
  | Capacitor size | 2fF~ 10pF  |
  | ENOB@ Nyquist rate  | >12bits  |
  | Sampling rate | >30MS/s  |
  | Walden figure-of-merit (FOM) | < 100-fJ/conversion-step  |

## Get Started

{{< figure src="adc1.png" title="High Level Block Diagram of the Pipelined SAR ADC" >}}

The diagram above shows the block diagram of the SAR ADC architecture. The ADC is a pipeline of a 6-bit and a 8-bit SAR ADCs. We decide to use differential sampling in order to cancel the common mode sampling offset. Furthermore, Vcm-based switching technique is used in both stages to lower the power consumption of the whole system.

{{< figure src="adcst1.png" title="Stage 1 Schematic Diagram" >}}

The first stage has 6-bit effective resolution. The first stage sub-ADC and CDAC share the same sampling capacitor array. There are several typical switching techniques that are available. We decide to use Vcm based switching technique mainly because the low power consumption and faster settling speed. However, one biggest drawback of this method is that it requires extra switches to control each capacitor. There are three possibilities at all sampling capacitors. Before the certain bit compared, the corresponding capacitor’s bottom plate is connected to Vcm. After comparison, its bottom plate will be connected to either ground or Vref depends on the comparing result is 1 or 0. Notice that the positive pair sampling capacitor array and the negative pair sampling capacitor array are connected opposite to each other. These sets of switches are controlled by a SAR logic unit which I'll go over in next section. Additional independent clock sets are used to make sure each capacitor is in the right phase. 

{{< figure src="adcst2.png" title="Stage 2 Schematic Diagram" >}}

The second stage is a 8-bit SAR ADC. The use of SAR architecture in the second stage enables a large resolution in this single stage. The implementation is very similar compare to the first stage but has two more capacitor sets. 


## SAR Logic
{{< figure src="sarlogic1.png" title="6-bit SAR Logic" >}}
The classic SAR architecture is use due to its straightforward design technique. Figure above is the implementation on Cadence. It consists of a set of ring counter and a set of shift regisiter. There are 2x6+2 = 14 D flip flops in use. For each conversion, piror to the first clock rising edge, RESET will first clocked high to reset all flip flop's output to 0. After that, the RESET signal remains low for the reset of the process. Once the first rising edge approaches, the MSB flip flop is set to 1. Then when second rising edge approaches, the counter shifts 1 to the next flip flop until it reaches the LSB. SAR logic determains the value of bit one by one based on the comparator's output. For a 6-bit SAR logic, it requires 1+6 = 7 cycles to complete one single conversion. Table below is the algorithm of 6-bit SAR logic.

  | Clock | D1| D2| D3| D4| D5| D6 | COMP. Out |
  | ------- |-|-|-|-|-| -| ------- |
  | RESET   | 0 |0| 0| 0 |0| 0       | -- |
  | 1       | 1| 0| 0| 0| 0| 0       | D1 |
  | 2       | D1 |1 |0 |0 |0 |0      | D2 |
  | 3       | D1 |D2 |1| 0 |0 |0     | D3 |
  | 4       | D1 |D2 |D3| 1 |0 |0    | D4 |
  | 5       | D1 |D2 |D3| D4 |1 |0   | D5 |
  | 6       | D1 |D2 |D3 |D4 |D5 |1  | D6 |
  | 7       | D1 |D2| D3 |D4| D5 |D6 | -- |
  








- 👉 [**Create a new site**](https://wowchemy.com/templates/)
- 📚 [**Personalize your site**](https://wowchemy.com/docs/)
- 💬 [Chat with the **Wowchemy community**](https://discord.gg/z8wNYzb) or [**Hugo community**](https://discourse.gohugo.io)
- 🐦 Twitter: [@wowchemy](https://twitter.com/wowchemy) [@GeorgeCushen](https://twitter.com/GeorgeCushen) [#MadeWithWowchemy](https://twitter.com/search?q=(%23MadeWithWowchemy%20OR%20%23MadeWithAcademic)&src=typed_query)
- 💡 [Request a **feature** or report a **bug** for _Wowchemy_](https://github.com/wowchemy/wowchemy-hugo-modules/issues)
- ⬆️ **Updating Wowchemy?** View the [Update Guide](https://wowchemy.com/docs/guide/update/) and [Release Notes](https://wowchemy.com/updates/)

## Crowd-funded open-source software

To help us develop this template and software sustainably under the MIT license, we ask all individuals and businesses that use it to help support its ongoing maintenance and development via sponsorship.

### [❤️ Click here to become a sponsor and help support Wowchemy's future ❤️](https://wowchemy.com/plans/)

As a token of appreciation for sponsoring, you can **unlock [these](https://wowchemy.com/plans/) awesome rewards and extra features 🦄✨**

## Ecosystem

* **[Hugo Academic CLI](https://github.com/wowchemy/hugo-academic-cli):** Automatically import publications from BibTeX

## Inspiration

[Check out the latest **demo**](https://academic-demo.netlify.com/) of what you'll get in less than 10 minutes, or [view the **showcase**](https://wowchemy.com/user-stories/) of personal, project, and business sites.

## Features

- **Page builder** - Create *anything* with [**widgets**](https://wowchemy.com/docs/page-builder/) and [**elements**](https://wowchemy.com/docs/writing-markdown-latex/)
- **Edit any type of content** - Blog posts, publications, talks, slides, projects, and more!
- **Create content** in [**Markdown**](https://wowchemy.com/docs/writing-markdown-latex/), [**Jupyter**](https://wowchemy.com/docs/import/jupyter/), or [**RStudio**](https://wowchemy.com/docs/install-locally/)
- **Plugin System** - Fully customizable [**color** and **font themes**](https://wowchemy.com/docs/customization/)
- **Display Code and Math** - Code highlighting and [LaTeX math](https://en.wikibooks.org/wiki/LaTeX/Mathematics) supported
- **Integrations** - [Google Analytics](https://analytics.google.com), [Disqus commenting](https://disqus.com), Maps, Contact Forms, and more!
- **Beautiful Site** - Simple and refreshing one page design
- **Industry-Leading SEO** - Help get your website found on search engines and social media
- **Media Galleries** - Display your images and videos with captions in a customizable gallery
- **Mobile Friendly** - Look amazing on every screen with a mobile friendly version of your site
- **Multi-language** - 34+ language packs including English, 中文, and Português
- **Multi-user** - Each author gets their own profile page
- **Privacy Pack** - Assists with GDPR
- **Stand Out** - Bring your site to life with animation, parallax backgrounds, and scroll effects
- **One-Click Deployment** - No servers. No databases. Only files.

## Themes

Wowchemy and its templates come with **automatic day (light) and night (dark) mode** built-in. Alternatively, visitors can choose their preferred mode - click the moon icon in the top right of the [Demo](https://academic-demo.netlify.com/) to see it in action! Day/night mode can also be disabled by the site admin in `params.toml`.

[Choose a stunning **theme** and **font**](https://wowchemy.com/docs/customization) for your site. Themes are fully customizable.

## License

Copyright 2016-present [Zhe Liu](zheliu0.com).
