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

/* Add spacing between filter buttons */
#opp-filters li {
  margin: 0.25rem 0.5rem 0.25rem 0; /* top/right/bottom/left */
}
#opp-filters .button {
  min-width: 10rem;       /* makes them wider and consistent */
  text-align: center;     /* centers text inside */
}

</style>

<script>
  (function () {
    const bar   = document.getElementById('opp-filters');
    if (!bar) return;

    const btns  = bar.querySelectorAll('[data-filter]');
    const cards = document.querySelectorAll('#opps .opp');

    function applyFilter(slug) {
      cards.forEach(card => {
        const cat = card.getAttribute('data-cat-slug');
        card.style.display = (slug === 'all' || cat === slug) ? '' : 'none';
      });
    }

    function setActive(targetBtn) {
      btns.forEach(b => b.classList.remove('special')); // remove active styling
      targetBtn.classList.add('special');               // theme’s highlighted look
    }

    // Click handling
    btns.forEach(btn => {
      btn.addEventListener('click', function (e) {
        e.preventDefault();
        const slug = this.getAttribute('data-filter');
        applyFilter(slug);
        setActive(this);
        // Optional: keep state in URL hash
        if (history && history.replaceState) history.replaceState(null, '', '#' + slug);
      });
    });

    // Initial state from URL hash (e.g., /opportunity#short-term-trip)
    const initialSlug = (location.hash || '#all').slice(1);
    const initBtn = bar.querySelector(`[data-filter="${initialSlug}"]`) || btns[0];
    setActive(initBtn);
    applyFilter(initBtn.getAttribute('data-filter'));
  })();
</script>

<!-- Tally popup script (only needed if using tally_id links) -->
<script async src="https://tally.so/widgets/embed.js"></script>