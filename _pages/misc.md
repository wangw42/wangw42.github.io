---
layout: archive
title: ""
permalink: /misc/
author_profile: true
sitemap: false
---

Miscellaneous.
===

{% include base_path %}
{% capture written_year %}'None'{% endcapture %}
{% for post in site.posts %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if year != written_year %}
    <h2 id="{{ year | slugify }}" class="archive__subtitle">{{ year }}</h2>
    {% capture written_year %}{{ year }}{% endcapture %}
  {% endif %}
  {% include archive-single.html %}
{% endfor %}



<!-- 
<style>
  .image-container {
    float: left;
    margin-right: 10px;
  }

  .image-container img {
    max-width: 255px;
    height: auto;
  }
</style>

<div class="image-container">
  <img src="../images/pipilu/pipilu1.jpg" />
</div>

<div class="image-container">
  <img src="../images/pipilu/pipilu2.jpg" />
</div>

<div class="image-container">
  <img src="../images/pipilu/pipilu3.jpg" />
</div>

<div class="image-container">
  <img src="../images/pipilu/pipilu4.jpg" />
</div>

<div class="image-container">
  <img src="../images/pipilu/pipilu5.jpg" />
</div>

<div class="image-container">
  <img src="../images/pipilu/pipilu6.JPG" />
</div>

<div class="image-container">
  <img src="../images/pipilu/pipilu8.JPG" />
</div>

<div class="image-container">
  <img src="../images/pipilu/pipilu9.jpg" />
</div>



<div style="clear: both;"></div> 
  -->