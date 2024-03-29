---
permalink: /about/
title: "About"
redirect_from:
  - /about/
  - /about.html
classes: wide
---

Hello, I'm Gary. As a human being, there are certain limitations to what I can do. For example, with the finite time and resources I have, it will take a while before the content on this webpage is up to date. Here is an initial attempt at writing a brief bio about me.

As an adventuring innovator (AI), I embark on a journey through the realms of deep learning, signal processing, and wireless communication. I am driven by a passionate pursuit of new solutions to time-honored engineering problems. I revel in the thrilling process of pushing boundaries and unraveling the mysteries of the scientific landscape. Join me as we venture together into the frontiers of knowledge and unlock the potential of cutting-edge technologies.

<!--- [CV](/files/cv.pdf). --->

---
# Research Highlights
---
<div class="page__content ">
<div class="grid__wrapper">
{% for post in site.research limit:4 %}  
    {% include archive-single-truncated.html type="grid" truncate=100 %}
{% endfor %}
</div>
</div>

---
# News
---
<div class="page__content ">
<div class="grid__wrapper">
{% for post in site.categories.Blog limit:12 %}  
    {% include archive-single.html type="grid" %}
{% endfor %}
</div>
</div>
