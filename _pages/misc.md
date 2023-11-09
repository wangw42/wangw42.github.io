---
layout: archive
title: ""
permalink: /misc/
author_profile: true
sitemap: false
---

Miscellaneous.
===

{%- if site.enable_project_categories and page.display_categories %} {%- for category in page.display_categories %}
{{ category }}
{%- assign categorized_posts = site.posts | where: "category", category -%} {%- assign sorted_posts = categorized_posts | sort: "importance" %} {% if page.horizontal -%}
{%- for project in sorted_posts -%} {% include posts_horizontal.html %} {%- endfor %}
{%- else -%}
{%- for project in sorted_posts -%} {% include posts.html %} {%- endfor %}
{%- endif -%} {% endfor %}
{%- else -%}

{%- assign sorted_posts = site.posts | sort: "importance" -%}

{% if page.horizontal -%}

{%- for project in sorted_posts -%} {% include posts_horizontal.html %} {%- endfor %}
{%- else -%}
{%- for project in sorted_posts -%} {% include posts.html %} {%- endfor %}
{%- endif -%} {%- endif -%}


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