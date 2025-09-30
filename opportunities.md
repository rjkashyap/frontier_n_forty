---
layout: page
title: Opportunities
description: Matthew 28:18-20
image: assets/images/pic01.jpg
nav-menu: false
show_tile: false
---


<h2>Current Opportunities</h2>

<!-- Card container -->
<div id="cards" class="card-grid"></div>

<!-- PapaParse to read CSV -->
<script src="https://cdn.jsdelivr.net/npm/papaparse@5.3.2/papaparse.min.js"></script>

<!-- Tally popup script -->
<script async src="https://tally.so/widgets/embed.js"></script>

<script>
  // Replace with your published Google Sheet CSV link
  const sheetUrl = "https://docs.google.com/spreadsheets/d/e/2PACX-1vSC4Ls6Bv9zrsIAcSczGHqXfG3fq4Wr4zFN0QBT106XM5-zAxSCvKbfSq9qtn9ENqJCmnO3OvdiMNIb/pub?gid=1421394344&single=true&output=csv";

  Papa.parse(sheetUrl, {
    download: true,
    header: true,
    complete: function(results) {
      const container = document.getElementById("cards");
      results.data.forEach(row => {
        // Only show published opportunities
        if(row.Title && row.Publish === "TRUE") {
          container.innerHTML += `
            <div class="card">
              <img src="${row.Image}" alt="${row.Title}">
              <h3>${row.Title}</h3>
              <p><strong>${row.Category}</strong> — ${row.Location}</p>
              <p>${row.Duration}</p>
              <p>${row.StartDate} → ${row.FinishDate}</p>
              <div class="summary">${row.Summary || ""}</div>
              <a href="#tally-open=${row.TallyID}&tally-overlay=1"
                 class="button fit"
                 role="button">
                 Apply Now
              </a>
            </div>
          `;
        }
      });
    }
  });
</script>

<style>
  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 2rem;
  }
  .card {
    border: 1px solid #ccc;
    border-radius: 12px;
    padding: 1rem;
    background: #fff;
    box-shadow: 0 2px 6px rgba(0,0,0,0.08);
  }
  .card img {
    width: 100%;
    height: 180px;
    object-fit: cover;
    border-radius: 8px;
    margin-bottom: .75rem;
  }
  .card h3 {
    margin: .5rem 0;
  }
  .card .button {
    display: inline-block;
    margin-top: .75rem;
    background: #0074d9;
    color: #fff;
    padding: .6rem 1.2rem;
    border-radius: 6px;
    text-decoration: none;
    font-weight: 600;
  }
  .card .button:hover {
    background: #005fa3;
  }
</style>