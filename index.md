---
title: Mobile Growth Notes
layout: page
---

Practical notes on mobile user acquisition and monetization — for app developers and UA managers.

<div class="cta-box">
  <strong>Need help with user acquisition or monetization?</strong><br>
  I help app developers lower CPI, improve retention, and fix ad revenue.<br>
  <a href="https://www.linkedin.com/in/mika-lee-0a920044a/">Connect on LinkedIn</a> · <a href="mailto:mikaabdalla1@gmail.com">Email me</a>
</div>

## What I write about

- **User acquisition** — CPI, ROAS, LTV, offerwall vs programmatic
- **App monetization** — eCPM, fill rate, mediation, in-app bidding
- **Market insights** — Southeast Asia, LATAM, US, Japan

## Latest posts

<div class="post-grid">
{% for post in site.posts %}
  <a class="post-card" href="{{ post.url | relative_url }}">
    {% if post.image %}<img class="post-card-img" src="{{ post.image | relative_url }}" alt="{{ post.title | escape }}">{% endif %}
    <span class="post-card-body">
      <span class="post-card-title">{{ post.title | escape }}</span>
      <span class="post-card-desc">{{ post.description | default: post.excerpt | strip_html | truncate: 140 }}</span>
    </span>
  </a>
{% endfor %}
</div>
