---
layout: page
title: Opportunities
permalink: /opportunity
nav-menu: false
show_tile: false
---

<div id="main" class="alt">
  <section id="ten">
    <div class="inner">

      <h2>Current Opportunities</h2>

      <!-- Category Filters -->
      <ul class="actions filters" id="opp-filters">
        <li><a href="#" class="button special" data-filter="all">All</a></li>
        <li><a href="#" class="button" data-filter="staff-role">Staff Role</a></li>
        <li><a href="#" class="button" data-filter="mission-internship">Mission Internship</a></li>
        <li><a href="#" class="button" data-filter="church-planting-residency">Church Planting Residency</a></li>
        <li><a href="#" class="button" data-filter="short-term-trip">Short-term Trip</a></li>
        <li><a href="#" class="button" data-filter="medium-term-placement">Medium-term Placement</a></li>
        <li><a href="#" class="button" data-filter="long-term-placement">Long-term Placement</a></li>
      </ul>

      <!-- Opportunities Grid -->
      <div id="opps">
        {% for opp in site.opportunities %}
          {% if opp.publish %}
            {% assign blurb = opp.excerpt
                              | default: opp.summary
                              | default: opp.content
                              | strip_html
                              | truncate: 220 %}

            {% assign cat_slug = opp.category | downcase
              | replace: ' ', '-'
              | replace: '&', 'and'
              | replace: '/', '-'
              | replace: '--', '-' %}

            <div class="opp" data-cat-slug="{{ cat_slug }}">

              {% if opp.drive_id %}
                <img
                  src="https://lh3.googleusercontent.com/d/{{ opp.drive_id }}=w1600"
                  alt="{{ opp.title | escape }}">
              {% endif %}

              <h3>{{ opp.title }}</h3>

              {% if opp.location %}
                <p class="location">📍 {{ opp.location }}</p>
              {% endif %}

              {% if blurb %}
                <p class="excerpt">{{ blurb }}</p>
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
                <ul class="actions">
                  <li>
                    <a href="#tally-open={{ opp.tally_id }}&tally-overlay=1"
                       class="button"
                       role="button">Apply Now</a>
                  </li>
                </ul>
              {% elsif opp.apply_now %}
                <ul class="actions">
                  <li>
                    <a href="{{ opp.apply_now }}"
                       class="button"
                       target="_blank" rel="noopener"
                       role="button">Apply Now</a>
                  </li>
                </ul>
              {% endif %}

            </div>
          {% endif %}
        {% endfor %}
      </div> <!-- /#opps -->

    </div>
  </section>
</div>

<style>
  /* Grid */
  #opps {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.25rem;
    margin-top: 1rem;
  }

  /* Card — square corners to match theme */
  #opps .opp {
    background: #161a22;
    color: #e6e9ef;
    border: 1px solid rgba(230,233,239,0.10);
    border-radius: 0;
    padding: 1rem;
    box-shadow: none;

    /* Fade animation for filter show/hide */
    opacity: 1;
    transform: translateY(0);
    transition: opacity .18s ease, transform .18s ease;
  }
  #opps .opp.is-hidden {
    opacity: 0;
    transform: translateY(6px);
  }

  /* Image — square corners, natural aspect */
  #opps .opp img {
    width: 100%;
    height: auto;
    display: block;
    border-radius: 0;
    margin-bottom: 0.5rem;
  }

  /* Text */
  #opps .opp h3 {
    margin: 0.25rem 0 0.25rem;
    line-height: 1.25;
    color: #ffffff;
  }
  #opps .opp .location {
    margin: 0 0 0.5rem;
    color: rgba(230,233,239,0.68);
    font-weight: 600;
  }
  #opps .opp .excerpt {
    margin: 0 0 0.5rem;
    color: rgba(230,233,239,0.68);
  }
  #opps .opp .meta {
    margin: 0 0 0.75rem;
    color: rgba(230,233,239,0.68);
    font-size: 0.95rem;
  }

  /* Filter toolbar spacing */
  #opp-filters { margin: .25rem 0 1rem; }
  #opp-filters li { margin: 0.25rem 0.5rem 0.25rem 0; }
  #opp-filters .button { min-width: 10rem; text-align: center; }
</style>

<script>
  (function () {
    const bar   = document.getElementById('opp-filters');
    if (!bar) return;

    const btns  = bar.querySelectorAll('[data-filter]');
    const cards = Array.from(document.querySelectorAll('#opps .opp'));
    const DURATION = 200; // ms, matches CSS ~ .18s

    function hideCard(card) {
      if (card.dataset.hidden === '1') return;
      card.dataset.hidden = '1';
      card.classList.add('is-hidden');
      setTimeout(() => { card.style.display = 'none'; }, DURATION);
    }

    function showCard(card) {
      if (card.dataset.hidden !== '1') return;
      card.style.display = '';
      void card.offsetWidth; // force reflow to allow transition
      card.classList.remove('is-hidden');
      delete card.dataset.hidden;
    }

    function applyFilter(slug) {
      cards.forEach(card => {
        const cat = card.getAttribute('data-cat-slug');
        const show = (slug === 'all' || cat === slug);
        if (show) showCard(card);
        else hideCard(card);
      });
    }

    function setActive(targetBtn) {
      btns.forEach(b => b.classList.remove('special'));
      targetBtn.classList.add('special'); // theme’s highlighted button
    }

    btns.forEach(btn => {
      btn.addEventListener('click', function (e) {
        e.preventDefault();
        const slug = this.getAttribute('data-filter');
        applyFilter(slug);
        setActive(this);
        if (history && history.replaceState) history.replaceState(null, '', '#' + slug);
      });
    });

    // Initial state from URL hash (e.g., /opportunity#short-term-trip)
    const initialSlug = (location.hash || '#all').slice(1);
    const initBtn = bar.querySelector(`[data-filter="${initialSlug}"]`) || btns[0];

    // Set initial visibility instantly (no animation on first paint)
    cards.forEach(card => {
      const cat = card.getAttribute('data-cat-slug');
      const visible = (initialSlug === 'all' || cat === initialSlug);
      if (!visible) {
        card.classList.add('is-hidden');
        card.style.display = 'none';
        card.dataset.hidden = '1';
      }
    });

    setActive(initBtn);
  })();
</script>

<!-- Tally popup script (needed for #tally-open links) -->
<script async src="https://tally.so/widgets/embed.js"></script>