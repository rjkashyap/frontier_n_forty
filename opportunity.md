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

				<ul>
				{% for opp in site.opportunities %}
					{% if opp.publish %}
					<li>
						<h3>{{ opp.title }}</h3>
						<p>{{ opp.excerpt }}</p>
						
						{% if opp.tally_id %}
						<a href="#tally-open={{ opp.tally_id }}&tally-overlay=1">Apply Now</a>
						{% elsif opp.apply_now %}
						<a href="{{ opp.apply_now }}" target="_blank" rel="noopener">Apply Now</a>
						{% endif %}
					</li>
					{% endif %}
				{% endfor %}
				</ul>

				<!-- Tally script (only needed if you use tally_id) -->
				<script async src="https://tally.so/widgets/embed.js"></script>	



			
			</div>
		</section>



</div>