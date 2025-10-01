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
					data-drive-id="{{ opp.drive_id }}"
					data-placeholder="{{ 'assets/images/opportunities/placeholder.png' | relative_url }}"
					alt="{{ opp.title | escape }}"
					onerror="driveImgFallback(this)"
				>
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
  /* === Dark palette tokens === */
  :root {
    --bg:        #0f1115;
    --bg-alt:    #161a22;
    --fg:        #e6e9ef;
    --fg-bold:   #ffffff;
    --fg-light:  rgba(230,233,239,0.68);
    --border:    rgba(230,233,239,0.10);
    --border-bg: rgba(230,233,239,0.05);
    --highlight: #7aa2ff;   /* accent1 */
    --accent1:   #7aa2ff;
    --accent2:   #a78bfa;
    --accent3:   #fca5a5;
    --accent4:   #f6d487;
    --accent5:   #93c5fd;
    --accent6:   #34d399;

    /* Button tokens */
    --btn-bg:    var(--highlight);
    --btn-fg:    var(--fg-bold);
    --btn-bg-h:  #5f86ff;   /* hover tint near highlight */
    --card-bg:   var(--bg-alt);
    --card-fg:   var(--fg);
  }

  /* Make the list a responsive grid */
  #opps {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.25rem;
    margin-top: 1rem;
  }

  /* Card */
  #opps .opp {
    background: var(--card-bg);
    color: var(--card-fg);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1rem;
    box-shadow: 0 2px 10px rgba(0,0,0,.25), inset 0 0 0 1px var(--border-bg);
  }

  /* Card image */
  #opps .opp img {
    width: 100%;
    height: 180px;
    object-fit: cover;
    display: block;
    border-radius: 8px;
    margin-bottom: 0.5rem;
  }

  /* Text */
  #opps .opp h3 {
    margin: 0.25rem 0 0.35rem;
    line-height: 1.25;
    color: var(--fg-bold);
  }
  #opps .opp .excerpt {
    margin: 0 0 0.75rem;
    color: var(--fg-light);
  }

  /* Buttons */
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

<script>
  function driveHiRes(id){ return `https://lh3.googleusercontent.com/d/${id}=w1600`; }
  function driveView(id){  return `https://drive.google.com/uc?export=view&id=${id}`; }
  function driveThumb(id){ return `https://drive.google.com/thumbnail?id=${id}&sz=w1200`; }

  function driveImgFallback(img){
    const id = img.dataset.driveId;
    const state = img.dataset.state || "hires";
    if(!id) return;

    if(state === "hires"){
      img.dataset.state = "view";
      img.src = driveView(id);
    } else if(state === "view"){
      img.dataset.state = "thumb";
      img.src = driveThumb(id);
    } else {
      img.onerror = null; // stop loops
      img.src = img.dataset.placeholder || "{{ '/images/opportunities/placeholder.jpg' | relative_url }}";
    }
  }
</script>

