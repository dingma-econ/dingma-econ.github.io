---
language: en
title: Curriculum Vitae
no_heading: true
---

{% capture cv_pdf %}{{ "/assets/CV_Ding_Ma_ENG.pdf" | relative_url }}?v={{ site.time | date: "%Y%m%d%H%M" }}{% endcapture %}
My curriculum vitae is available as a PDF. You can read it below, open it in a new tab, or download a copy.

<p class="cv-buttons">
<a class="btn btn-cv btn-lg" href="{{ cv_pdf }}" target="_blank" rel="noopener">Open CV (PDF)</a>
<a class="btn btn-default btn-lg" href="{{ cv_pdf }}" download="CV_Ding_Ma.pdf">Download CV</a>
</p>

<div class="cv-embed">
<iframe src="{{ cv_pdf }}#view=FitH" title="Curriculum Vitae of Ding Ma (PDF)"></iframe>
</div>
