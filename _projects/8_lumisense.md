---
layout: page
title: LumiSense
description: Sensing-guided cannula for safer deep anterior lamellar keratoplasty
img: assets/img/projects/lumisense.png
importance: 8
category: past
---

{% include figure.liquid loading="eager" path="assets/img/projects/lumisense_problem.png" title="Hand tremor exceeds the DALK safety margin. The Descemet's membrane safe zone is 10–15 µm; the manual tremor envelope is roughly 100 µm. Figure created by Waverly Rose Brim." class="img-fluid rounded z-depth-1" %}

Deep anterior lamellar keratoplasty (DALK) is preferred over full-thickness corneal transplant because it preserves the patient's own endothelium and lowers graft rejection risk. The procedure depends on dissecting a ~500 µm stroma down to a 10–15 µm margin above Descemet's membrane, by hand, with an unassisted tremor envelope roughly 7–10× that margin. Published manual perforation rates run from 4% to 39%, and a perforation typically means intraoperative conversion to the procedure the surgeon was trying to avoid.

**Need statement.** Corneal surgeons need a way to accurately determine and control incision depth during keratoplasty in order to prevent unintended damage to adjacent tissue.

## Concept

LumiSense is a handheld DALK cannula that closes the loop between depth sensing and needle advancement. A sensing element at the tip reads stromal depth in real time, an on-board model estimates proximity to Descemet's membrane, and a hardware safety stop prevents the needle from advancing past the safe margin. Loss of power, signal, or software all resolve to the same outcome: the needle cannot move.

{% include figure.liquid loading="eager" path="assets/img/projects/lumisense.gif" title="CAD render of the LumiSense handpiece. Render created by Waverly Rose Brim." class="img-fluid rounded z-depth-1" %}

## Quick facts

<div class="table-responsive">
<table class="table table-sm">
  <tbody>
    <tr><th scope="row">Procedure</th><td>Deep anterior lamellar keratoplasty (DALK)</td></tr>
    <tr><th scope="row">Failure mode addressed</th><td>Descemet's membrane perforation</td></tr>
    <tr><th scope="row">Form factor</th><td>Handheld, reusable body with disposable tip, no external console</td></tr>
    <tr><th scope="row">Sensing</th><td>Fiber-based optical depth measurement at the cannula tip</td></tr>
    <tr><th scope="row">Inference</th><td>On-device tissue-layer segmentation</td></tr>
    <tr><th scope="row">Safety</th><td>Fail-secure mechanical stop at the safe-margin threshold</td></tr>
    <tr><th scope="row">Regulatory concept</th><td>Class II, De Novo pathway</td></tr>
  </tbody>
</table>
</div>

## Why it matters

Current tools leave the depth decision entirely to the surgeon: adjustable trephines offer no feedback, and microscope-integrated OCT shows depth but does not act on it. Robotic and laser platforms address precision but carry capital costs that most ambulatory surgery centers cannot justify for this procedure. The target is a capital-light instrument that fits an existing sterile tray, adds no OR time, and gives the surgeon a physical guarantee rather than a screen to watch.

## My role

I served as the AI and technical lead (CTO role) on a five-person team in Johns Hopkins EN.585.702, Medical Device Innovation and Design (Spring 2025). I owned the sensing-to-inference-to-actuation system architecture, the on-device segmentation model concept, the end-to-end latency and safety-actuation design, and all device renders and clinical figures.

**Team.** Ramya Tangirala, Roshni Parikh, Ava Stadler, Matthew Pack, Waverly Rose Brim. Advisors: Soumyadipta Acharya, MD, MSE, PhD; Shameema Sikder, MD; Swaroop Vedula.

## Status

Concept and design stage. The technical approach, control logic, and validation plan are not published here.
