---
layout: page
title: SCRUB
description: Surgical gloved-hand pose estimation
img: assets/img/projects/scrub.jpg
importance: 1
category: current
---

{% include figure.liquid loading="eager" path="assets/img/projects/scrub.jpg" title="Clinical motivation for SCRUB" class="img-fluid rounded z-depth-1" %}


Surgical pose estimation has historically focused on bare-hand keypoint detection. Operating rooms are bare-hand-free environments; surgeons wear gloves, which break the visual assumptions modern pose models rely on. SCRUB is a computer vision system designed to close that gap.

I'm developing SCRUB as part of my graduate research at Johns Hopkins, with downstream applications in surgical skill assessment, intraoperative workflow analytics, and automated technique evaluation.

**Why it matters.** Reliable hand pose estimation in the OR is a prerequisite for any computer vision system that wants to reason about what surgeons are _doing_ — not just where they're standing. Gloves, blood, instruments, and partial occlusion are the actual operating conditions, and they're systematically underrepresented in benchmarks.

**Status.** Accepted to the WiML Symposium at ICML 2026. Code release planned alongside the MICCAI 2027 submission window.
