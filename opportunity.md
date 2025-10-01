---
layout: opportunity
title: Opportunities
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
            {% assign blurb = opp.excerpt
                              | default: opp.summary
                              | default: opp.content
                              | strip_html
                              | truncate: 220 %}

            <div class="opp">

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
                       class="button special"
                       role="button">Apply Now</a>
                  </li>
                </ul>
              {% elsif opp.apply_now %}
                <ul class="actions">
                  <li>
                    <a href="{{ opp.apply_now }}"
                       class="button special"
                       target="_blank" rel="noopener"
                       role="button">Apply Now</a>
                  </li>
                </ul>
              {% endif %}

            </div>
          {% endif %}
        {% endfor %}
      </div>

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

  /* Buttons: use theme defaults (white buttons, square corners) via .button */

/* Make the image link feel interactive */
#opps .opp a.js-open-opp {
  display: block;
  position: relative;
  outline: none;
}

#opps .opp a.js-open-opp img {
  transition: transform .18s ease, filter .18s ease;
}

/* Hover/focus: slight lift + dim for contrast */
#opps .opp a.js-open-opp:hover img,
#opps .opp a.js-open-opp:focus img {
  cursor: pointer;
  transform: translateY(-2px);
  filter: brightness(0.92);
}

/* Optional: add a faint overlay on hover/focus (no rounded corners) */
#opps .opp a.js-open-opp::after {
  content: "";
  position: absolute;
  inset: 0;
  background: rgba(255,255,255,0);
  transition: background .18s ease;
}
#opps .opp a.js-open-opp:hover::after,
#opps .opp a.js-open-opp:focus::after {
  background: rgba(255,255,255,0.04);
}

/* ===== Modal base ===== */
.modal { 
  position: fixed; 
  inset: 0; 
  display: none; 
  z-index: 1000; 
}
.modal.is-open { display: block; }

/* Backdrop */
.modal__backdrop {
  position: absolute;
  inset: 0;
  background: rgba(0,0,0,.6);
}

/* Dialog */
.modal__dialog {
  position: relative;
  z-index: 1;
  max-width: 720px;
  margin: 6vh auto;
  background: #161a22; /* matches your card bg */
  color: #e6e9ef;
  border: 1px solid rgba(230,233,239,0.10);
  padding: 1.25rem;
  border-radius: 0;     /* square corners to match theme */
}

/* Close (X) */
.modal__close {
  position: absolute;
  top: .5rem;
  right: .75rem;
  background: transparent;
  border: 0;
  font-size: 1.5rem;
  color: #e6e9ef;
  cursor: pointer;
}

/* Image inside modal */
.modal__image-wrap img {
  width: 100%;
  height: auto;
  display: block;
  margin-bottom: .75rem;
}

/* Meta + summary */
#opp-modal .meta {
  color: rgba(230,233,239,0.68);
  margin: .25rem 0 .75rem;
}

</style>

<script>
  // Format YYYY-MM-DD to "MMM DD, YYYY"
  function fmtDate(d) {
    if (!d) return "";
    try { return new Date(d).toLocaleDateString(undefined, { year:'numeric', month:'short', day:'2-digit' }); }
    catch(e){ return d; }
  }

  const modal = document.getElementById('opp-modal');
  const img   = document.getElementById('opp-modal-img');
  const title = document.getElementById('opp-modal-title');
  const meta  = document.getElementById('opp-modal-meta');
  const sum   = document.getElementById('opp-modal-summary');
  const acts  = document.getElementById('opp-modal-actions');

  function openModalFrom(el){
    const d = el.dataset;

    // Title
    title.textContent = d.title || '';

    // Meta line
    const parts = [];
    if (d.location) parts.push('📍 ' + d.location);

    const dates =
      (d.start ? fmtDate(d.start) : '') +
      (d.finish ? ' → ' + fmtDate(d.finish) : '');

    const hasDates = !!(d.start || d.finish);
    const duration = d.duration || '';

    const mid = [dates, (hasDates && duration ? ' • ' : '') + duration].join('').trim();
    meta.textContent = [parts.join(''), (parts.length && mid ? ' • ' : '') + mid].join('');

    // Summary
    sum.textContent = d.summary || '';

    // Image
    if (d.drive) {
      img.src = `https://lh3.googleusercontent.com/d/${d.drive}=w1600`;
      img.style.display = '';
    } else {
      img.removeAttribute('src');
      img.style.display = 'none';
    }

    // Actions (Apply)
    acts.innerHTML = '';
    if (d.tally) {
      const li = document.createElement('li');
      const a  = document.createElement('a');
      a.className = 'button';
      a.textContent = 'Apply Now';
      a.href = `#tally-open=${d.tally}&tally-overlay=1`;
      li.appendChild(a);
      acts.appendChild(li);
    }

    // Show modal
    modal.classList.add('is-open');
    modal.setAttribute('aria-hidden', 'false');
  }

  function closeModal(){
    modal.classList.remove('is-open');
    modal.setAttribute('aria-hidden', 'true');
  }

  // Delegated clicks
  document.addEventListener('click', (e) => {
    const openEl = e.target.closest('.js-open-opp');
    if (openEl) {
      e.preventDefault();
      openModalFrom(openEl);
      return;
    }
    const closeEl = e.target.closest('.js-close-opp');
    if (closeEl || e.target === document.querySelector('#opp-modal .modal__backdrop')) {
      e.preventDefault();
      closeModal();
    }
  });

  // ESC to close
  document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape' && modal.classList.contains('is-open')) closeModal();
  });
</script>

<!-- Tally popup script (needed for #tally-open links) -->
<script async src="https://tally.so/widgets/embed.js"></script>

<!-- Tally popup script (only needed if using tally_id links) -->
<script async src="https://tally.so/widgets/embed.js"></script>