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
                <img src="https://drive.google.com/thumbnail?id={{ opp.drive_id }}" alt="{{ opp.title | escape }}">
              {% endif %}

              <h3>{{ opp.title }}</h3>
              <p>{{ opp.excerpt }}</p>

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
  /* === Your palette as CSS variables === */
  :root {
    --bg:        #0f1115;
    --bg-alt:    #161a22;
    --fg:        #e6e9ef;
    --fg-bold:   #ffffff;
    --fg-light:  rgba(230,233,239,0.68);
    --border:    rgba(230,233,239,0.10);
    --border-bg: rgba(230,233,239,0.05);
    --highlight: #7aa2ff;  /* also accent1 */
    --accent1:   #7aa2ff;
    --accent2:   #a78bfa;
    --accent3:   #fca5a5;
    --accent4:   #f6d487;
    --accent5:   #93c5fd;
    --accent6:   #34d399;

    /* Button tokens */
    --btn-bg:    var(--highlight);
    --btn-fg:    var(--fg-bold);
    --btn-bg-h:  #5f86ff; /* hover tint close to highlight */
    --btn-bdr:   var(--border);
  }

  #opps .opp img {
    max-width: 100%;
    height: auto;
    display: block;
    margin-bottom: 0.5rem;
    border-radius: 6px;
  }
  #opps .opp {
    margin-bottom: 2rem;
  }

  /* Button styles (fallback if theme lacks .button classes) */
  .button {
    display: inline-block;
    padding: .65rem 1.1rem;
    border-radius: 8px;
    text-decoration: none;
    font-weight: 600;
    text-align: center;
    border: 1px solid var(--btn-bdr);
    transition: transform .04s ease, filter .12s ease, box-shadow .12s ease;
  }
  .button.primary {
    background: var(--btn-bg);
    color: var(--btn-fg);
    box-shadow: 0 4px 10px rgba(122,162,255,0.25);
  }
  .button.primary:hover {
    background: var(--btn-bg-h);
    filter: brightness(1);
    transform: translateY(-1px);
    box-shadow: 0 6px 14px rgba(122,162,255,0.32);
  }
  .button.fit { width: 100%; }
</style>
