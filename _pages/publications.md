---
layout: page
permalink: /publications/
title: publications
description: Peer-reviewed publications in neuro-oncology AI, medical imaging, and clinical machine learning.
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

<div class="publications">

<h3>Journal Articles</h3>

{% bibliography --query @article[note!=Correspondence] %}

<h3>Book Chapters</h3>

{% bibliography --query @incollection %}

<h3>Conference Abstracts and Proceedings</h3>

{% bibliography --query @inproceedings %}

<h3>Correspondence</h3>

{% bibliography --query @article[note=Correspondence] %}

</div>
