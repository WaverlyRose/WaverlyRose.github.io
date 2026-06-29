---
layout: page
title: SCRUB
description: Feature collapse and partial signal recovery in gloved-hand pose estimation
img: assets/img/projects/scrub.jpg
importance: 1
category: current
---

{% include figure.liquid loading="eager" path="assets/img/projects/scrub_qualitative.png" title="Off-the-shelf tracking fails on a real gloved frame. white_surgical example (id 34506): MediaPipe detects no hand (no red), SCRUB (blue) tracks against ground truth (green). Example success case, not typical: PCK@20 0.92 here vs. a 36.17% average." class="img-fluid rounded z-depth-1" %}

<div class="card my-4">
  <div class="card-body">
    <div class="row align-items-center text-center justify-content-center g-0">
      <div class="col">
        <div class="display-3 fw-bold">0.00%</div>
        <div class="text-muted">MediaPipe Hands</div>
      </div>
      <div class="col-auto display-4 text-muted px-3">&rarr;</div>
      <div class="col">
        <div class="display-3 fw-bold text-primary">36.17%</div>
        <div class="text-muted">SCRUB</div>
      </div>
    </div>
    <p class="text-center text-muted mb-0 mt-2">PCK@20 on the <code>white_surgical</code> cell, identical images and ground truth</p>
  </div>
</div>

On the real-glove `white_surgical` cell, MediaPipe Hands returns 0.00% PCK@20 while SCRUB returns 36.17% on identical images and ground truth (95% CI [31.51, 40.81]), under a pre-registered paired image-level bootstrap (10,000 resamples, seed 42). This is not a better number for its own sake: it separates _no landmarks at all_ from _present, recoverable landmarks_.

## Contributions

- Identifies **feature collapse** as the failure mechanism: surgical gloves alter the image's frequency distribution rather than simply degrading quality.
- A **frequency-domain analysis** (amplitude spectrum and radial decay) that explains why modern heatmap regressors fail under gloves.
- A **pre-registered paired evaluation protocol** comparing SCRUB and MediaPipe on identical images, ground-truth keypoints, and validity masks.
- A strong **HRNet-W32 + Adaptive Wing baseline** that outperforms several domain-adaptation strategies under feature collapse.
- **Partial signal recovery** as a foundation for future sterile gesture interfaces, framed as motivation rather than a current clinical capability.

## Quick facts

<div class="table-responsive">
<table class="table table-sm">
  <tbody>
    <tr><th scope="row">Task</th><td>2D hand pose estimation</td></tr>
    <tr><th scope="row">Domain</th><td>Operating room (gloved hands)</td></tr>
    <tr><th scope="row">Input</th><td>RGB images</td></tr>
    <tr><th scope="row">Output</th><td>21 hand keypoints</td></tr>
    <tr><th scope="row">Backbone</th><td>HRNet-W32</td></tr>
    <tr><th scope="row">Loss</th><td>Adaptive Wing Loss</td></tr>
    <tr><th scope="row">Evaluation</th><td>PCK@20, paired image-level bootstrap</td></tr>
    <tr><th scope="row">Datasets</th><td>FreiHAND, MC-Hands, Surgical Hands</td></tr>
  </tbody>
</table>
</div>

## Why it matters

Operating rooms are bare-hand-free environments. Surgeons wear gloves, replacing varied skin texture with a uniform, often specularly reflective surface that breaks the assumptions modern pose models rely on. In sterile fields, clinicians also cannot touch input devices without breaking sterility, so touchless gesture control is one of the few viable modalities. Reliable gloved-hand pose estimation is the missing prerequisite.

{% include figure.liquid loading="eager" path="assets/img/projects/scrub.jpg" title="Clinical motivation for SCRUB" class="img-fluid rounded z-depth-1" %}

Longer term, the same signal could support surgical skill assessment and intraoperative workflow analytics. SCRUB does **not** do those things today; they remain motivations for closing the gloved-hand gap, not claims about current capability.

## Mechanism

Gloving is a structural change to the input. Gloves redistribute high-frequency image energy into diffuse, low-information patterns, so the structured texture that heatmap regression relies on disappears and the detector collapses instead of degrading gracefully. A frequency-domain view makes this concrete: the amplitude spectrum and its radial decay carry relatively more mid-to-high-radius energy under gloves, consistent with a diffuse spectrum rather than a clean high-frequency cutoff.

{% include figure.liquid loading="eager" path="assets/img/projects/scrub_mechanism.png" title="Feature collapse: amplitude spectrum, fingertip heatmap, and backbone channels for bare vs. gloved hands" class="img-fluid rounded z-depth-1" %}

{% include figure.liquid loading="eager" path="assets/img/projects/scrub_radial_decay.png" title="Radial decay of the luminance spectrum: the gloved profile carries relatively more mid-to-high-radius energy" class="img-fluid rounded z-depth-1" %}

## Experimental evidence

SCRUB is evaluated along two disclosed tracks. The first is an internal checkpoint-selection ablation across eight variants (A–H). The second is a pre-registered paired image-level bootstrap against MediaPipe, holding images, ground-truth keypoints, and keypoint-validity masks fixed across both systems, with a directional claim permitted only when the 95% CI excludes zero.

On the gloved subset (`white_*`, n = 745), SCRUB reaches 30.54% PCK@20 versus 8.73% for MediaPipe (+21.82 pp, 95% CI [19.25, 24.48]). The mixed surface (n = 5,630: 88.52% vs. 32.87%) is supporting context only: it is dominated by bare-hand imagery and is not the headline.

### Negative result

No standard domain-adaptation family beat a carefully tuned HRNet-W32 + Adaptive Wing baseline. Augmentation stacking over-regularizes; adversarial feature alignment (DANN) costs roughly 40 pp on the internal surface; and CycleGAN synthesis only partially offsets the stacking penalty. Under feature collapse, added complexity consistently underperformed careful optimization. Reporting this openly is part of the contribution.

## Approach

At a high level, SCRUB trains an HRNet-W32 backbone with Adaptive Wing Loss on a three-dataset, 21-keypoint corpus: FreiHAND (bare-hand geometry), MC-Hands<sup>[2](#ref-2)</sup> (synthetic gloves), and Surgical Hands (real OR imagery, with procedure-grouped splits). Against this baseline it tests eight variants spanning a custom augmentation stack, CycleGAN bare-to-gloved synthesis, and DANN feature alignment. Components are named deliberately; the training recipe is held for publication.

{% include figure.liquid loading="eager" path="assets/img/projects/scrub_pipeline.png" title="End-to-end SCRUB pipeline: three-dataset corpus, HRNet-W32 + AWing, and the paired evaluation against MediaPipe" class="img-fluid rounded z-depth-1" %}

## Current limitations

This is partial signal recovery, not a solution. 36.17% PCK@20 is not clinical-grade, and gloved MPJPE remains 59.3 mm, so error stays large. The real-OR imagery used here is honest stress, but it is not a task-matched, front-facing gloved-webcam endpoint. The mechanistic figures use illustrative bare-versus-gloved pairs rather than identity-matched subjects.

## Future directions

The largest gap is a public, subject-disjoint gloved-webcam benchmark with frontal geometry and standardized 21-point labels. Beyond that: harmonized detection semantics across MediaPipe and heatmap heads, identity-matched mechanistic capture to support the spectral claims, and closing the real-time interaction path on the recovered signal.

## Status

- Accepted to the WiML Symposium at ICML 2026.
- Manuscript in preparation for the MICCAI 2027 submission window.
- Code release planned after the MICCAI 2027 submission.
- Public gloved-webcam benchmark in early development.

## Collaboration

I'm building toward a public gloved-webcam benchmark and am open to collaborators or OR data partners.

## Citation

```bibtex
@misc{brim2026scrub,
  title  = {SCRUB: Feature Collapse and Partial Signal Recovery in Gloved-Hand Pose Estimation},
  author = {Brim, Waverly Rose},
  year   = {2026},
  note   = {Work in progress; accepted to the WiML Symposium at ICML 2026}
}
```

## References

1. N. Louis, L. Zhou, S. J. Yule, R. D. Dias, M. Manojlovich, F. D. Pagani, D. S. Likosky, and J. J. Corso, “Temporally guided articulated hand pose tracking in surgical videos,” _International Journal of Computer Assisted Radiology and Surgery_, vol. 17, pp. 1–9, 2022. [Dataset: Surgical Hands](https://github.com/MichiganCOG/Surgical_Hands_RELEASE)

2. <a id="ref-2"></a>P. Boutis, Z. Batzos, K. Konstantoudakis, A. Dimou, and P. Daras, “MC-hands-1M: A glove-wearing hand dataset for pose estimation,” arXiv:2210.10428, 2022. [Dataset](https://zenodo.org/records/7194271)

3. C. Zimmermann, D. Cremers, et al., “FreiHAND: A dataset for markerless capture of hand pose and shape from single RGB images,” in _Proc. IEEE/CVF ICCV_, 2019, pp. 813–822.

4. F. Zhang, A. Bazarevsky, A. Vakunov, A. Tkachenka, G. Sung, C.-L. Chang, and A. Grundmann, “MediaPipe Hands: On-device real-time hand tracking,” arXiv:2006.10214, 2020.

5. K. Sun, B. Xiao, D. Liu, and J. Wang, “Deep high-resolution representation learning for human pose estimation,” in _Proc. IEEE/CVF CVPR_, 2019, pp. 5693–5703.

6. X. Wang, L. Bo, and F. Li, “Adaptive Wing Loss for robust face alignment via heatmap regression,” in _Proc. IEEE/CVF ICCV_, 2019, pp. 6971–6981.

7. P. Chattopadhyay, K. Sarangmath, V. Vijaykumar, and J. Hoffman, “PASTA: Proportional amplitude spectrum training augmentation for syn-to-real domain generalization,” in _Proc. IEEE/CVF ICCV_, 2023, pp. 19288–19300.

8. J. Tobin, R. Fong, A. Ray, J. Schneider, W. Zaremba, and P. Abbeel, “Domain randomization for transferring deep neural networks from simulation to the real world,” arXiv:1703.06907, 2017.

9. J.-Y. Zhu, T. Park, P. Isola, and A. A. Efros, “Unpaired image-to-image translation using cycle-consistent adversarial networks,” in _Proc. IEEE ICCV_, 2017, pp. 2223–2232.

10. F. Mueller, D. Mehta, O. Sridhar, D. Cremers, and S. Sridhar, “GANerated hands for real-time 3D hand tracking from monocular RGB,” in _Proc. IEEE/CVF CVPR_, 2018, pp. 49–59.

11. A. Kirillov, E. Mintun, N. Ravi, et al., “Segment anything,” in _Proc. IEEE/CVF ICCV_, 2023, pp. 4015–4026.

12. Y. Ganin and V. Lempitsky, “Unsupervised domain adaptation by backpropagation,” in _Proc. ICML_, 2015, pp. 1180–1189.

13. A. W. Kiefer et al., “Enhanced 2D hand pose estimation for gloved medical applications: A preliminary model,” _Sensors_, vol. 24, no. 18, art. 6005, 2024.

14. R. Papo et al., “RoHan: Robust hand detection in the operating room,” arXiv:2501.08115, 2025.

15. A. Mewes et al., “Touchless interaction with software in interventional radiology and surgery: A systematic literature review,” _International Journal of Computer Assisted Radiology and Surgery_, vol. 12, no. 2, pp. 291–305, 2017.

16. G. Casiez, N. Roussel, and D. Vogel, “1 € filter: A simple speed-based low-pass filter for noisy input in interactive systems,” in _Proc. ACM CHI_, 2012, pp. 2527–2530.
