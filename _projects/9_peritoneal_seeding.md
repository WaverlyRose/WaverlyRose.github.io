---
layout: page
title: Peritoneal Seeding Detection
description: Intraoperative decision support for biopsy selection in diagnostic laparoscopy
img: assets/img/projects/peritoneal_thumbnail.png
importance: 9
category: past
---

<figure>
  <img src="{{ 'assets/img/projects/peritoneal_prototype.gif' | relative_url }}" class="img-fluid rounded z-depth-1" width="100%" height="auto" alt="Prototype decision-support overlay on laparoscopic video. Mockup, not a validated clinical output." title="Prototype decision-support overlay on laparoscopic video. Mockup, not a validated clinical output." loading="eager">
</figure>

Gastric cancer is the fifth most common malignancy and the fourth leading cause of cancer death worldwide, and approximately 20% of patients present with peritoneal metastasis ([Ilic and Ilic, 2022](https://doi.org/10.3748/wjg.v28.i12.1187)). Peritoneal involvement is a contraindication for gastrectomy and redirects management toward systemic therapy, which makes accurate intraperitoneal staging a prerequisite for surgical decision-making. Diagnostic laparoscopy remains the reference standard: the surgeon inspects the peritoneum, biopsies suspicious nodules, and awaits frozen-section pathology before proceeding.

The procedure is limited by the visual ambiguity of the target. Benign and malignant peritoneal nodules are frequently indistinguishable under white-light laparoscopy, adhesions obscure the field, and each biopsy introduces bleeding risk and a frozen-section turnaround that extends operative time at an estimated $35–50 per minute. In practice, surgeons sample multiple nodules to compensate for diagnostic uncertainty, at the cost of longer procedures and variable accuracy, and false-negative sampling can lead to a gastrectomy in a patient with occult peritoneal disease.

**Need statement.** A way to address wrongful biopsies in diagnostic laparoscopy for the staging of patients with gastric cancer: fewer biopsies, higher diagnostic accuracy, shorter operative time.

## Concept

A segmentation model that runs on the laparoscopic feed and flags nodule regions by likelihood of malignancy, so the surgeon can prioritize which nodules to sample rather than sampling everything. The tool sits alongside frozen section as decision support; it does not replace pathology.

<figure>
  <img src="{{ 'assets/img/projects/peritoneal_pipeline.gif' | relative_url }}" class="img-fluid rounded z-depth-1" width="100%" height="auto" alt="From laparoscopic video to frame-level nodule segmentation" title="From laparoscopic video to frame-level nodule segmentation" loading="eager">
</figure>

## Data

The proposal is built around a multi-institution laparoscopic video corpus of peritoneal nodules with pathology-confirmed labels, sourced through collaborating surgical societies across the gastric cancer and general laparoscopy communities. The core of the labeling problem is the ontology: a benign nodule and a malignant one can share color, texture, and vascularity, and the distinction only exists at the level of histology.

{% include figure.liquid loading="eager" path="assets/img/projects/peritoneal_ontology.png" title="Labeling ontology: malignant versus benign peritoneal nodules under white-light laparoscopy" class="img-fluid rounded z-depth-1" %}

## Quick facts

<div class="table-responsive">
<table class="table table-sm">
  <tbody>
    <tr><th scope="row">Procedure</th><td>Diagnostic laparoscopy for gastric cancer staging</td></tr>
    <tr><th scope="row">Task</th><td>Nodule segmentation with malignancy likelihood</td></tr>
    <tr><th scope="row">Input</th><td>Laparoscopic RGB video</td></tr>
    <tr><th scope="row">Output</th><td>Per-nodule masks, color-coded by risk; frame-level summary</td></tr>
    <tr><th scope="row">Ground truth</th><td>Frozen section and permanent pathology</td></tr>
    <tr><th scope="row">Validation plan</th><td>Surgeon reader study, then a single-center prospective safety and feasibility cohort</td></tr>
  </tbody>
</table>
</div>

## Why it matters

Every avoided biopsy is avoided bleeding risk and avoided frozen-section wait. More importantly, a missed malignant nodule sends a patient to a gastrectomy they should not have had, and a false positive denies one to a patient who could have benefited. The value of the tool is in steering the biopsy, not in making the diagnosis.

## My role

Team project at the 4th Surgical Data Science Summer School, IHU Strasbourg (2025). I led the computer vision design: the segmentation formulation, the application workflow from model output to surgeon-facing overlay, and the prototype interface shown above.

**Team.** Waverly Rose Brim (Johns Hopkins), Kendall Feeny (UCL), Matthijs Fitski (Princess Máxima Center), Hoseok Seo (Catholic Medical Center / University of Toronto), Cameron Reid (Duke), Santhi Raj Kolamuri (Dr. NTR UHS), Saurav Sharma (IHU Strasbourg), Daichi Kitaguchi (University of Tsukuba).

## Status

Concept and prototype stage. Model architecture, training details, and results are not published here.
