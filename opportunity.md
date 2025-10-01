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
                <a href="#tally-open={{ opp.tally_id }}&tally-overlay=1">Apply Now</a>
              {% elsif opp.apply_now %}
                <a href="{{ opp.apply_now }}" target="_blank" rel="noopener">Apply Now</a>
              {% endif %}

            </div>
          {% endif %}
        {% endfor %}
      </div>

    </div>
  </section>
</div>

<style>
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
</style>

