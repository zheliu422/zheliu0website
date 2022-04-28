---
title: "An 84dB-SNDR Low-OSR 4th-Order Noise-Shaping SAR with an FIA-Assisted EF-CRFF Structure and Noise-Mitigated Push-Pull Buffer-in-Loop Technique"
authors:
- Tzu-Han Wang
- Tian Xie
- admin
- Shaolan Li
author_notes:
- "Equal contribution"
- "Equal contribution"
date: "2022-02-01T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2021-02-10T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "IEEE International Solid-State Circuits Conference (ISSCC) 2022, accepted"
publication_short: "ISSCC 2022"

Supplementary notes can be found here, including our ISSCC 2022 [Presentation](https://github.com/zheliu422/Supporting_File/blob/main/NSSAR_slide.pdf), and the main page on [IEEE Xplore](https://ieeexplore.ieee.org/abstract/document/9731771).

abstract: With the combined merits of the SAR and the ΔΣ ADCs, the noise-shaping (NS) SAR architecture can achieve high resolution with a mild OSR, making it versatile for a wide range of applications. Nonetheless, designing a highly power-efficient NS-SAR under relatively low OSRs (<8) can be challenging. It requires the design to concurrently address two key considerations. The first is to implement high-order optimized NS with simple and low-power hardware that maximally preserves a SAR’s efficient nature. In this regard, two recent works report 4th-order NS using a cascaded EF structure [1] and an FVF-assisted CIFF structure [2] respectively, both allowing aggressive NTFs to be realized with simple open-loop amps. However, they still employ static amps/buffers, which limit the power improvement. Also, the lack of NTF optimization makes them nonideal for low OSR designs. The second concern is the growing kT/C noise contribution under low OSR and the related large stress on the input driver. To alleviate this issue, ref [3] presents an NS-SAR with a loop-embedded input buffer that decouples the input capacitance from the kT/C noise constraint; but it suffers from large noise penalty introduced by the buffer and the separated CDAC. Alternatively, a sampling noise cancellation (SNC) technique is proposed in [4] to facilitate a smaller CDAC value. However, owing to imperfect cancellation caused by circuit non-idealities, the CDAC can remain considerably large.

tags:
- ADC
- ISSCC
featured: false

# links:
# - name: ""
#   url: ""
url_pdf: ''
url_code: ''
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**ISSCC.org**](https://www.isscc.org/)'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---

{{% callout note %}}
Click the *PDF * button above to see the work.
{{% /callout %}}
{{% callout note %}}
Click the *Cite * button above to import publication metadata into your reference management software.
{{% /callout %}}

