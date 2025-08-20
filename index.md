---
layout: default
title: Human Resources Data Visualization Dashboard
---

{% comment %}
Render README from “Business Requirements vs. Customer Needs” (fallback “## Summary”).
Strip the README’s own mobile About-card block; then inject:
  Summary → Back to top (mobile-only) → faint divider → About (mobile card) → Back to top (mobile-only) → Table of Contents.
On desktop/wide, keep only the README’s inline Back to top (classed) and the hero’s desktop About card.
{% endcomment %}

{% capture readme_raw %}{% include_relative README.md %}{% endcapture %}

{% assign token_car = '## Business Requirements vs. Customer Needs' %}
{% assign token_summary = '## Summary' %}
{% if readme_raw contains token_car %}{% assign start_token = token_car %}{% else %}{% assign start_token = token_summary %}{% endif %}

{% assign after_start = readme_raw | split: start_token %}
{% if after_start.size > 1 %}
  {% capture body_from_start %}{{ start_token }}{{ after_start[1] }}{% endcapture %}
{% else %}
  {% assign body_from_start = readme_raw %}
{% endif %}

{% assign toc_parts = body_from_start | split: '## Table of Contents' %}
{% assign pre_toc = toc_parts[0] %}
{% assign post_toc = toc_parts[1] %}

{%- comment -%}
Remove the README’s own mobile About-card (it starts with this comment in README).
Everything between that marker and the Table of Contents is dropped; we’ll inject our own.
{%- endcomment -%}
{% assign strip_mobile_marker = '<!-- ===== Mobile-only Author Card injected AFTER the story section ===== -->' %}
{% if pre_toc contains strip_mobile_marker %}
  {% assign pre_toc = pre_toc | split: strip_mobile_marker | first %}
{% endif %}

{%- capture back_orig -%}<div align="right"><a href="#site-top">↑ Back to top</a></div>{%- endcapture -%}
{%- capture back_classed -%}<div class="car-backlink" align="right"><a href="#site-top">↑ Back to top</a></div>{%- endcapture -%}
{% assign car_html = pre_toc | replace: back_orig, back_classed %}

{{ car_html | markdownify }}

<!-- Mobile/compact-only: Back to top BETWEEN Summary and About -->
<div class="backlink--injected" align="right"><a href="#site-top">↑ Back to top</a></div>
<hr class="m-divider" />

<!-- Mobile/compact-only About the Author -->
<div class="author-card author-card--mobile">
  <div class="author-card__heading">About the Author</div>

  <a href="{{ site.author_photo }}" target="_blank" rel="noopener">
    <img class="author-card__photo" src="{{ site.author_photo }}" alt="{{ site.author }}">
  </a>

  <div class="author-card__name">{{ site.author }}</div>
  {% if site.author_title %}<div class="author-card__title">{{ site.author_title }}</div>{% endif %}
  {% if site.author_subtitle %}<div class="author-card__subtitle">{{ site.author_subtitle }}</div>{% endif %}

  <div class="author-card__links">
    {% for l in site.author_links %}
      <a class="author-card__btn" href="{{ l.url | escape }}" target="_blank" rel="noopener noreferrer">
        {{ l.icon }} {{ l.label }}
      </a>
    {% endfor %}
  </div>
</div>

<!-- Mobile/compact-only: Back to top AFTER About -->
<div class="backlink--after-author" align="right"><a href="#site-top">↑ Back to top</a></div>

{% if post_toc %}
  {% capture rest %}## Table of Contents{{ post_toc }}{% endcapture %}
  {{ rest | markdownify }}
{% endif %}


