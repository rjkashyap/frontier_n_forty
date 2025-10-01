---
layout: page
title: Opportunities
description: Matthew 28:18-20
image: assets/images/pic01.jpg
permalink: /opportunity
nav-menu: false
show_tile: false
---

<div id="main" class="alt">
  <section id="ten">
    <div class="inner">

      <h2>Current Opportunities</h2>

      <div id="opps">
        {% for opp in site.opportunities %}
          {% if opp.publish %}
            <div class="opp">

              {% if opp.drive_id %}
                <img
                  src="https://lh3.googleusercontent.com/d/{{ opp.drive_id }}=w1600"
                  alt="{{ opp.title | escape }}"
                >
              {% endif %}

              <h3>{{ opp.title }}</h3>

              {% if opp.location %}
                <p class="location">📍 {{ opp.location }}</p>
              {% endif %}

              {% if opp.excerpt %}
                <p class="excerpt">{{ opp.excerpt }}</p>
              {% endif %}

              {% assign has_dates = opp.start_date or opp.finish_date %}
              {% if has_dates or opp.duration %}
                <p class="meta">
                  {% if opp.start_date %}{{ opp.start_date | date: "%b %d, %Y" }}{% endif %}
                  {% if opp.finish_date %} → {{ opp.finish_date | date: "%b %d, %Y" }}{% endif %}
                  {% if opp.duration %}{% if has_dates %} • {% endif %}{{ opp.duration }}{% endif %}
                </p>
              {% endif %}

              {% if opp.tally_id %}
                <a href="#tally-open={{ opp.tally_id }}&tally-overlay=1"
                   class="button primary fit"
                   role="button">Apply Now</a>
              {% elsif opp.apply_now %}
                <a href="{{ opp.apply_now }}"
                   class="button primary fit"
                   target="_blank" rel="noopener"
                   role="button">Apply Now</a>
              {% endif %}

            </div>
          {% endif %}
        {% endfor %}
      </div>

    </div>
  </section>
</div>

<style>
  /* === Dark palette tokens === */
  :root {
    --bg:        #0f1115;
    --bg-alt:    #161a22;
    --fg:        #e6e9ef;
    --fg-bold:   #ffffff;
    --fg-light:  rgba(230,233,239,0.68);
    --border:    rgba(230,233,239,0.10);
    --border-bg: rgba(230,233,239,0.05);
    --highlight: #7aa2ff;
    --btn-bg:    var(--highlight);
    --btn-fg:    var(--fg-bold);
    --btn-bg-h:  #5f86ff;
    --card-bg:   var(--bg-alt);
    --card-fg:   var(--fg);
  }

  #opps {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.25rem;
    margin-top: 1rem;
  }

  #opps .opp {
    background: var(--card-bg);
    color: var(--card-fg);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1rem;
    box-shadow: 0 2px 10px rgba(0,0,0,.25), inset 0 0 0 1px var(--border-bg);
  }

  #opps .opp img {
    width: 100%;
    height: 180px;
    object-fit: cover;
    display: block;
    border-radius: 8px;
    margin-bottom: 0.5rem;
  }

  #opps .opp h3 {
    margin: 0.25rem 0 0.25rem;
    line-height: 1.25;
    color: var(--fg-bold);
  }

  #opps .opp .location {
    margin: 0 0 0.5rem;
    color: var(--fg-light);
    font-weight: 600;   /* a touch of emphasis */
  }

  #opps .opp .excerpt {
    margin: 0 0 0.5rem;
    color: var(--fg-light);
  }

  #opps .opp .meta {
    margin: 0 0 0.75rem;
    color: var(--fg-light);
    font-size: 0.95rem;
  }

  .button {
    display: inline-block;
    padding: .65rem 1.1rem;
    border-radius: 8px;
    text-decoration: none;
    font-weight: 600;
    text-align: center;
    border: 1px solid var(--border);
    transition: transform .04s ease, filter .12s ease, box-shadow .12s ease;
  }
  .button.primary {
    background: var(--btn-bg);
    color: var(--btn-fg);
    box-shadow: 0 4px 12px rgba(122,162,255,0.28);
  }
  .button.primary:hover {
    background: var(--btn-bg-h);
    transform: translateY(-1px);
    box-shadow: 0 6px 16px rgba(122,162,255,0.38);
  }
  .button.fit { width: 100%; }
</style>

<!-- Tally popup script (needed if you use tally_id) -->
<script async src="https://tally.so/widgets/embed.js"></script>