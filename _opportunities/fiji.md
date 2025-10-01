---
title: "Short-term Mission Trip to Fiji"
category: "Short-term Trip"
location: "Suva, Fiji"
start_date: 2025-07-01
finish_date: 2025-07-14
duration: "2 weeks"
drive_id: "1qeSug8EpSk6J4uW5hLOVpM_HP2Hp9K4p"  # <-- just the ID
tally_id: nr7QJL
publish: true
---

{% if page.image %}
  <!-- Use your existing direct image path/URL -->
  <img
    src="{{ page.image | relative_url }}"
    alt="{{ page.title | escape }}"
    style="max-width:100%;height:auto;display:block;margin-bottom:1rem;border-radius:6px;"
  >
{% elsif page.drive_id %}
  <!-- Fallback to Google Drive thumbnail (higher size for better quality) -->
  <img
    src="https://drive.google.com/thumbnail?id={{ page.drive_id }}&sz=w1200"
    alt="{{ page.title | escape }}"
    style="max-width:100%;height:auto;display:block;margin-bottom:1rem;border-radius:6px;"
  >
{% endif %}

Come with us to Fiji to serve communities and share the gospel. This trip will include training, outreach, and fellowship.

<a
  href="#tally-open={{ page.tally_id }}&tally-align-left=1&tally-overlay=1&tally-emoji-text=✈️&tally-emoji-animation=tada"
  class="button primary fit"
  role="button"
>Apply Now</a>