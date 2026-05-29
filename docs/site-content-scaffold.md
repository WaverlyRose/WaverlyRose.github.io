# al-folio site content scaffold — Waverly Rose Brim

This file bundles every piece of content for the initial site build. Each section below is marked with a `## File: <path>` header and contains the exact content to write to that path inside the al-folio repo.

After Cursor processes this file, there are three manual tasks at the end (image assets, _config.yml updates, BibTeX bulk completion).

---

## File: `_pages/about.md`

```markdown
I'm an AI research engineer working at the intersection of foundation models and biological data. My focus is computer vision and clinical decision systems — building production ML that lives where surgeons, radiologists, and pathologists actually work.

Currently at Yale Neurosurgery, where I own an end-to-end LLM/RAG service deployed in spine tumor boards: Go-based orchestration, FastAPI/Pydantic, Postgres/pgvector retrieval on EKS, FHIR-like structured outputs with citation grounding. Concurrently developing SCRUB at Johns Hopkins, a computer vision system for surgical gloved-hand pose estimation, and an Apple Silicon–optimized port of MindEye2 for fMRI-to-image reconstruction.

Earlier work spans multimodal computational pathology and genomics in meningioma (Yale Neurosurgery, Gunel Lab), real-time surgical skill assessment via computer vision (Hopkins Malone Center), and genetically encoded voltage indicators engineered on a DARPA-funded neural engineering program (Yale, Pieribone Lab). 20+ peer-reviewed publications, concentrated in systematic reviews of AI in neurooncology.

Finishing an M.S. in Artificial Intelligence at Johns Hopkins Whiting School of Engineering (December 2026). Research interests: multimodal foundation models, biomedical representation learning, clinical decision systems, and computational pathology.

Based in the New York Metropolitan area.
```

---

## File: `_projects/1_scrub.md`

```markdown
---
layout: page
title: SCRUB
description: Surgical gloved-hand pose estimation
img: assets/img/projects/scrub.jpg
importance: 1
category: current
---

Surgical pose estimation has historically focused on bare-hand keypoint detection. Operating rooms are bare-hand-free environments — surgeons wear gloves, which break the visual assumptions modern pose models rely on. SCRUB is a computer vision system designed to close that gap.

I'm developing SCRUB as part of my graduate research at Johns Hopkins, with downstream applications in surgical skill assessment, intraoperative workflow analytics, and automated technique evaluation.

**Why it matters.** Reliable hand pose estimation in the OR is a prerequisite for any computer vision system that wants to reason about what surgeons are *doing* — not just where they're standing. Gloves, blood, instruments, and partial occlusion are the actual operating conditions, and they're systematically underrepresented in benchmarks.

**Status.** Submitted to the WiML Symposium at ICML 2026. Code release planned alongside the MICCAI 2027 submission window.
```

---

## File: `_projects/2_spine_rag.md`

```markdown
---
layout: page
title: Spine Oncology RAG Service
description: Production LLM/RAG system for spine tumor boards
img: assets/img/projects/spine-rag.jpg
importance: 2
category: current
---

A privacy-safe LLM/RAG service deployed in spine tumor boards at Yale Neurosurgery. The system converts raw clinical context — imaging impressions, pathology reports, surgical history, guideline literature — into one-page briefs that accelerate oncologic decision-making.

**System.** Go-based orchestration and S3 streaming I/O behind FastAPI/Pydantic, deployed on Kubernetes (EKS) with Postgres/pgvector retrieval. Outputs FHIR-like structured JSON with inline citations to source documents. SRE-grade Grafana dashboards expose latency, reliability, and reasoning-trace observability so model behavior stays auditable.

**Role.** End-to-end ownership across model integration, evaluation tooling, retrieval iteration, deployment, and incident response. Cross-functional work spans neurosurgeons, data scientists, and engineers.

**Why it matters.** Most clinical LLM deployments stop at notebook demos. This one lives in an actual tumor board workflow, with the observability and structured outputs needed for guidance to be decision-ready rather than demo-grade.
```

---

## File: `_projects/3_mindeye2.md`

```markdown
---
layout: page
title: MindEye2-Demo
description: Apple Silicon port of fMRI-to-image reconstruction
img: assets/img/projects/mindeye.jpg
importance: 3
category: current
github: https://github.com/WaverlyRose/mindeye2-demo
---

MindEye2 (Scotti et al., ICML 2024) reconstructs natural images from fMRI brain activity using diffusion models. The original implementation requires GPU clusters and 20+ GB of RAM. I rebuilt the pipeline to run on an Apple Silicon laptop.

**Approach.** Subject-specific linear aligners → residual MLP backbone (4-block with LayerNorm) → diffusion prior with DDIM sampling and FiLM conditioning → unCLIP/SDXL decoder. Reduced hidden dimensions (1024 vs 4096), shared residual blocks across the backbone, native Metal Performance Shaders support, and a modular three-notebook structure for the full voxel→features→tokens→image pipeline.

**Result.** ~40M parameters vs ~200M+ in the original. <6GB RAM vs 20+ GB. 10–15 seconds inference on an M3 MacBook vs hours on GPU clusters. Maintains >90% of original reconstruction quality. Uses real NSD (Natural Scenes Dataset) voxels — not synthetic data.

**Why it matters.** Frontier multimodal research is increasingly cluster-bound. Educational implementations that preserve the core method while running on accessible hardware lower the on-ramp for everyone trying to actually understand and extend this work.

[Code on GitHub](https://github.com/WaverlyRose/mindeye2-demo) · [Original paper](https://arxiv.org/abs/2403.11207)
```

---

## File: `_projects/4_soft_knn.md`

```markdown
---
layout: page
title: Soft-kNN ICU Mortality
description: Subgroup-fair calibration for ICU mortality prediction on MIMIC-IV
img: assets/img/projects/soft-knn.jpg
importance: 4
category: current
---

ICU mortality prediction models on MIMIC-IV routinely exhibit calibration gaps across demographic subgroups — race in particular shows a recurring worst-group AUROC floor that standard imputation methods don't help close. This project tests whether soft-kNN imputation combined with propensity-weighted training can raise that floor without sacrificing aggregate performance.

**Approach.** Soft-kNN imputation over EHR features; propensity-weighted loss for subgroup calibration; bootstrap confidence intervals on global AUROC; honest framing of race worst-group AUROC as a floor-raise rather than clinical-grade subgroup performance.

**Status.** Manuscript in preparation. Target venue: AAAI 2027 (full paper deadline late July). CHIL 2027 as backup.
```

---

## File: `_projects/5_meningioma.md`

```markdown
---
layout: page
title: Meningioma Multimodal Pipeline
description: Computational pathology and genomics for tumor microenvironments
img: assets/img/projects/meningioma.jpg
importance: 5
category: past
---

End-to-end pipelines fusing whole-slide pathology, microscopy, and multicenter genomic data to characterize meningioma tumor microenvironments — from wet-lab sample preparation through scalable batch inference and quantitative validation.

**Built.** Classical computer vision and machine learning workflows for subcellular structure detection and segmentation. High-throughput utilities to parse heterogeneous multicenter genomic datasets into standardized, analysis-ready dataframes and visualizations.

**Role.** Postgraduate Researcher in the Gunel Lab, Yale Neurosurgery (November 2021 – March 2025). Owned the full stack from sample preparation and immunohistochemistry through whole-slide digitization, data QC, and reproducible Python-based analysis.

**Why it matters.** Cross-site genomic interpretation in meningioma is bottlenecked by data heterogeneity. Standardizing the pipeline removed days of per-cohort prep work and made downstream comparative analyses tractable.
```

---

## File: `_projects/6_circlage.md`

```markdown
---
layout: page
title: Circlage
description: Real-time surgical skill assessment via computer vision
img: assets/img/projects/circlage.jpg
importance: 6
category: past
---

A computer vision platform for surgical skill assessment and operating room efficiency analytics, developed for deployment at Johns Hopkins Hospital and the University of Maryland Medical Center.

**Built.** Engineered early product and model foundations as R&D Engineer in the AI for Surgery Lab Startup at the Hopkins Malone Center. Prototyped an RNN-based surgical case duration prediction capability and designed administrator-facing analytics: forecasted durations, OR utilization trends, cost/earnings rollups, and staffing signals.

**Design.** Built human-in-the-loop feedback paths so UI interactions produce higher-quality labels — turning end-user workflow into training data that improves downstream computer vision performance over time.

**Role.** R&D Engineer, October 2023 – December 2024. Operated as the technical bridge between surgeons, OR administrators, and engineers.
```

---

## File: `_projects/7_gevi.md`

```markdown
---
layout: page
title: Genetically Encoded Voltage Indicators
description: Neural decoding under the DARPA NESD program
img: assets/img/projects/gevi.jpg
importance: 7
category: past
---

Genetically encoded voltage indicators (GEVIs) are protein-based biosensors that transduce membrane potential dynamics into quantifiable fluorescence. I engineered and validated GEVIs at the John B. Pierce Laboratory (now New Haven Innovation Labs) on the Pentagon's DARPA Neural Engineering System Design program.

**Work.** Rapid design–build–test cycles for biosensor variants: primer design, mutagenesis, plasmid construction, AAV vector production, and signal validation in neuronal systems. Operated core molecular and cellular workflows (PCR, gel electrophoresis, site-directed mutagenesis, primary neuronal culture) and supported in vivo / tissue-level validation including precision vibratome sectioning and organ-scale imaging.

**Pivot.** The lab's high-throughput imaging requirements pushed me into computation and automation — and ultimately into machine learning and computer science. This is where the AI side of my career started.

**Role.** Research Associate, January 2019 – August 2020.
```

---

## File: `_news/announcement_1.md`

```markdown
---
layout: post
date: 2026-05-15
inline: true
related_posts: false
---

Submitted SCRUB (surgical gloved-hand pose estimation) to the WiML Symposium at ICML 2026.
```

---

## File: `_news/announcement_2.md`

```markdown
---
layout: post
date: 2026-03-15
inline: true
related_posts: false
---

Manuscript in preparation on soft-kNN imputation for subgroup-fair ICU mortality prediction on MIMIC-IV. Target venue: AAAI 2027.
```

---

## File: `_news/announcement_3.md`

```markdown
---
layout: post
date: 2025-11-20
inline: true
related_posts: false
---

Released [MindEye2-Demo](https://github.com/WaverlyRose/mindeye2-demo): an Apple Silicon–optimized port of MindEye2 (Scotti et al., ICML 2024) for fMRI-to-image reconstruction.
```

---

## File: `_news/announcement_4.md`

```markdown
---
layout: post
date: 2025-07-15
inline: true
related_posts: false
---

Completed the Surgical Data Science Summer School at the Institute of Image-Guided Surgery (IHU Strasbourg).
```

---

## File: `_news/announcement_5.md`

```markdown
---
layout: post
date: 2025-03-31
inline: true
related_posts: false
---

Concluded postgraduate research on multimodal meningioma characterization in the Gunel Lab at Yale Neurosurgery.
```

---

## File: `_news/announcement_6.md`

```markdown
---
layout: post
date: 2025-01-15
inline: true
related_posts: false
---

Spine oncology LLM/RAG service shipped to Yale Neurosurgery tumor boards.
```

---

## File: `_bibliography/papers.bib`

> Note: This contains only the four "selected" publications to start. After Cursor writes this file, run the bulk import prompt at the bottom of this scaffold to populate the remaining ~16 entries from the Google Scholar PDF.

```bibtex
@article{jekel2022machine,
  title={Machine learning applications for differentiation of glioma from brain metastasis—a systematic review},
  author={Jekel, Leon and Brim, Waverly Rose and von Reppert, Marc and Staib, Lawrence and Cassinelli Petersen, Gabriel and others},
  journal={Cancers},
  volume={14},
  number={6},
  pages={1369},
  year={2022},
  selected={true},
  abbr={Cancers}
}

@article{petersen2022machine,
  title={Machine learning in differentiating gliomas from primary CNS lymphomas: A systematic review, reporting quality, and risk of bias assessment},
  author={Cassinelli Petersen, Gabriel I and Shatalov, J and Verma, T and Brim, Waverly Rose and Subramanian, H and others},
  journal={American Journal of Neuroradiology},
  volume={43},
  number={4},
  pages={526--533},
  year={2022},
  selected={true},
  abbr={AJNR}
}

@article{bahar2022machine,
  title={Machine learning models for classifying high-and low-grade gliomas: a systematic review and quality of reporting analysis},
  author={Bahar, Ryan C and Merkaj, Sabine and Cassinelli Petersen, Gabriel I and Tillmanns, Niklas and Subramanian, Harry and Brim, Waverly Rose and others},
  journal={Frontiers in Oncology},
  volume={12},
  pages={856231},
  year={2022},
  selected={true},
  abbr={Frontiers}
}

@article{lost2023systematic,
  title={Systematic literature review of machine learning algorithms using pretherapy radiologic imaging for glioma molecular subtype prediction},
  author={Lost, Jan and Verma, Tej and Jekel, Leon and von Reppert, Marc and Tillmanns, Niklas and Merkaj, Sabine and Brim, Waverly Rose and others},
  journal={American Journal of Neuroradiology},
  volume={44},
  number={10},
  pages={1126--1134},
  year={2023},
  selected={true},
  abbr={AJNR}
}
```

---

## File: `_pages/talks.md`

```markdown
---
layout: page
title: talks
permalink: /talks/
nav: true
nav_order: 4
---

### 2025
- **Surgical Data Science Summer School** — Institute of Image-Guided Surgery (IHU Strasbourg). Participant.

### 2021
- **AANS Diversity Task Force** — on fostering opportunity in neurosurgery. [Recording](https://www.youtube.com/watch?v=GlKFUqlyLao)

### Earlier
- **World Economic Forum** — Global Shapers Community programming.
```

> When the AfroTech HealthStack contract signs, add this block at the top of the talks list:
>
> ```markdown
> ### 2026
> - **AfroTech Conference** — HealthStack track. *Invited speaker.*
> ```

---

## Manual follow-ups (Cursor cannot do these from this scaffold alone)

### 1. Update `_config.yml`

Set the site `description` field to:

```
AI research engineer at Yale Neurosurgery and Johns Hopkins. Computer vision, foundation models, clinical decision systems.
```

Also confirm `first_name: Waverly`, `middle_name: Rose`, `last_name: Brim`, `email: wrb@waverlyrose.io`, `url: https://waverlyrose.io`, and social handles (LinkedIn, GitHub `WaverlyRose`, Google Scholar `VwZLAXoAAAAJ`) are populated.

### 2. Project images

Each project page references `assets/img/projects/<slug>.jpg`. Drop one image per project:

- `scrub.jpg` — system or architecture diagram (placeholder OK until paper figure is ready)
- `spine-rag.jpg` — clean architecture diagram of the service
- `mindeye.jpg` — use the reconstruction comparison figure from the MindEye2-Demo README
- `soft-knn.jpg` — calibration plot or schematic
- `meningioma.jpg` — pathology / whole-slide visualization
- `circlage.jpg` — dashboard mockup or OR vision schematic
- `gevi.jpg` — fluorescence imaging or biosensor schematic

### 3. Bulk BibTeX import (run as a separate Cursor agent prompt)

After this scaffold is processed, run this prompt to populate the rest of the publication list:

> Read `/mnt/project/_Waverly_Rose_Brim____Google_Scholar_.pdf`. Generate BibTeX entries for every publication listed there that is **not already present** in `_bibliography/papers.bib`. Use the same field format as the existing entries (`title`, `author`, `journal`, `volume`, `number`, `pages`, `year`, `abbr`). For each new entry, do NOT add `selected={true}`. Append the new entries to the end of `papers.bib`. After writing, list each new BibTeX key created.
