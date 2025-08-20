---
layout: default
title: Human Resources Data Visualization Dashboard
---

{% comment %}
Render README starting at “Business Requirements vs. Customer Needs” (fallback to “## Summary”),
then split at “## Table of Contents”.

- On desktop/wide: keep the README’s inline “Back to top” after the Summary.
- On mobile/compact: hide that inline one and inject a new Back to top + a faint divider
  BETWEEN the Summary and the mobile About card (to match Project 1).
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

{% assign toc_split = body_from_start | split: '## Table of Contents' %}

{%- capture back_orig -%}<div align="right"><a href="#site-top">↑ Back to top</a></div>{%- endcapture -%}
{%- capture back_classed -%}<div class="car-backlink" align="right"><a href="#site-top">↑ Back to top</a></div>{%- endcapture -%}

{% if toc_split.size > 1 %}
  {% assign car_with_class = toc_split[0] | replace: back_orig, back_classed %}
  {{ car_with_class | markdownify }}

  <!-- Mobile/compact-only Back to top + faint divider injected BEFORE About card -->
  <div class="backlink--injected" align="right"><a href="#site-top">↑ Back to top</a></div>
  <hr class="m-divider" />

  <!-- Mobile About card (appears only at mobile/compact via CSS) -->
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

  {% capture rest %}## Table of Contents{{ toc_split[1] }}{% endcapture %}
  {{ rest | markdownify }}
{% else %}
  {% assign car_with_class = body_from_start | replace: back_orig, back_classed %}
  {{ car_with_class | markdownify }}

  <div class="backlink--injected" align="right"><a href="#site-top">↑ Back to top</a></div>
  <hr class="m-divider" />

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
{% endif %}

