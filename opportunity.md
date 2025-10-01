---
layout: page
title: Opportunities
description: Matthew 28:18-20
image: assets/images/pic01.jpg
permalink: /opportunities/
nav-menu: false
show_tile: false
---

<div id="main" class="alt">

        <section id="ten">
            <div class="inner">



				<h2>Current Opportunities</h2>

				<div class="opportunities-grid">
				{%- comment -%}
				Sort newest Start Date first; fall back to title if no date
				{%- endcomment -%}
				{%- assign items = site.opportunities | sort: "start_date" | reverse -%}

				{%- for opp in items -%}
					{%- if opp.publish -%}
					{%- assign img = opp.image | default: "/images/opportunities/placeholder.jpg" -%}
					<article class="card">
						<div class="card-media">
						<img src="{{ img | relative_url }}" alt="{{ opp.title | escape }}">
						{%- if opp.category -%}
							<span class="badge">{{ opp.category }}</span>
						{%- endif -%}
						</div>

						<div class="card-body">
						<h3 class="card-title">{{ opp.title }}</h3>
						<p class="muted">
							{%- if opp.location -%}{{ opp.location }}{%- endif -%}
							{%- if opp.duration and opp.location -%} • {%- endif -%}
							{%- if opp.duration -%}{{ opp.duration }}{%- endif -%}
						</p>

						{%- if opp.start_date or opp.finish_date -%}
							<p class="muted">
							{%- if opp.start_date -%}{{ opp.start_date | date: "%b %d, %Y" }}{%- endif -%}
							{%- if opp.finish_date -%} → {{ opp.finish_date | date: "%b %d, %Y" }}{%- endif -%}
							</p>
						{%- endif -%}

						<div class="summary">
							{{ opp.excerpt | default: opp.content | markdownify }}
						</div>

						{%- comment -%}
						Prefer Tally popup via tally_id; otherwise fall back to apply_now URL.
						{%- endcomment -%}
						{%- if opp.tally_id -%}
							<a
							href="#tally-open={{ opp.tally_id }}&tally-overlay=1"
							class="button primary fit"
							role="button"
							>Apply Now</a>
						{%- elsif opp.apply_now -%}
							<a
							href="{{ opp.apply_now }}"
							class="button primary fit"
							target="_blank" rel="noopener"
							>Apply Now</a>
						{%- endif -%}
						</div>
					</article>
					{%- endif -%}
				{%- endfor -%}
				</div>

				<!-- Tally popup (once on the page if you use tally_id) -->
				<script async src="https://tally.so/widgets/embed.js"></script>

				<style>
				.opportunities-grid {
					display: grid;
					grid-template-columns: repeat(auto-fit, minmax(280px,1fr));
					gap: 1.25rem;
					margin-top: 1.5rem;
				}
				.card {
					display: flex; flex-direction: column;
					background: #fff; border: 1px solid #ddd; border-radius: 12px;
					overflow: hidden; box-shadow: 0 2px 8px rgba(0,0,0,.06);
				}
				.card-media { position: relative; }
				.card-media img {
					width: 100%; height: 200px; object-fit: cover; display: block;
				}
				.badge {
					position: absolute; left: 12px; top: 12px;
					background: #111; color: #fff; font-size: .75rem; padding: .25rem .5rem;
					border-radius: 999px;
				}
				.card-body { padding: 1rem; }
				.card-title { margin: 0 0 .25rem; font-size: 1.1rem; }
				.muted { color: #666; margin: 0 0 .25rem; }
				.summary p { margin-top: .5rem; }
				.button {
					display: inline-block; margin-top: .75rem; padding: .6rem 1rem;
					border-radius: 8px; text-decoration: none; font-weight: 600;
					background: #16a34a; color: #fff; text-align: center;
				}
				.button:hover { filter: brightness(.95); }
				.fit { width: 100%; }
				@media (max-width: 480px){
					.card-media img { height: 180px; }
				}
				</style>

								

						</section>

</div>

</div>