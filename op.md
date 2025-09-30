---
layout: page
title: Opportunities
permalink: /opportunities/
image: assets/images/pic01.jpg
nav-menu: false
show_tile: false
---

<div id="main" class="alt">

        <section id="ten">
			<div class="inner">
					<header class="major">
						<h2>Current Opportunities</h2>
					</header>
				
				
					<div class="row">



							<h2>Current Opportunities</h2>

							<div class="opportunities-grid">
							{% for opp in site.opportunities %}
								{% if opp.publish %}
								<div class="card">
									<img src="{{ opp.image }}" alt="{{ opp.title }}">
									<h3>{{ opp.title }}</h3>
									<p><strong>{{ opp.category }}</strong> — {{ opp.location }}</p>
									<p>{{ opp.start_date | date: "%b %d, %Y" }} → {{ opp.finish_date | date: "%b %d, %Y" }}</p>
									<p>{{ opp.duration }}</p>
									<div class="summary">
									{{ opp.content | markdownify }}
									</div>
									<a
									href="#tally-open={{ opp.tally_id }}&tally-align-left=1&tally-overlay=1&tally-emoji-text=✈️&tally-emoji-animation=tada"
									class="button primary fit"
									role="button"
									>Apply Now</a>
								</div>
								{% endif %}
							{% endfor %}
							</div>
					
					</div>   



					
        	</div>



		 

				

        </section>

</div>