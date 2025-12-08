---
layout: page
title: Compare Artworks
permalink: /compare/
---

## Compare Artworks Side-by-Side

Select two artworks from the collection to compare them side-by-side. This tool helps you explore connections, themes, and differences across the collection.

<div class="comparison-tool-standalone" style="margin: 30px 0;">
  <div class="comparison-controls" style="margin-bottom: 20px;">
    <select id="compare-artwork-1" class="compare-select" style="padding: 10px; margin-right: 10px; border-radius: 4px; border: 1px solid #ccc; min-width: 250px;">
      <option value="">Select first artwork...</option>
      {% for item in site.syrian_refugee_art %}
        <option value="{{ item.pid }}">{{ item.title }} - {{ item.artist }}</option>
      {% endfor %}
    </select>
    
    <select id="compare-artwork-2" class="compare-select" style="padding: 10px; margin-right: 10px; border-radius: 4px; border: 1px solid #ccc; min-width: 250px;">
      <option value="">Select second artwork...</option>
      {% for item in site.syrian_refugee_art %}
        <option value="{{ item.pid }}">{{ item.title }} - {{ item.artist }}</option>
      {% endfor %}
    </select>
    
    <button onclick="compareArtworks()" class="btn-compare" style="padding: 10px 24px; background-color: #0066cc; color: white; border: none; border-radius: 4px; cursor: pointer; font-weight: bold;">
      Compare
    </button>
    
    <button onclick="clearComparison()" class="btn-clear" style="padding: 10px 24px; background-color: #6c757d; color: white; border: none; border-radius: 4px; cursor: pointer; margin-left: 10px;">
      Clear
    </button>
  </div>
  
  <div id="comparison-results" style="display: none;">
    <div class="comparison-grid" style="display: grid; grid-template-columns: 1fr 1fr; gap: 30px; margin-top: 30px;">
      <div id="artwork-1-details" class="comparison-item" style="padding: 20px; background-color: #f8f9fa; border-radius: 8px; border: 2px solid #dee2e6;"></div>
      <div id="artwork-2-details" class="comparison-item" style="padding: 20px; background-color: #f8f9fa; border-radius: 8px; border: 2px solid #dee2e6;"></div>
    </div>
    
    <div class="comparison-insights" id="comparison-insights" style="margin-top: 30px; padding: 20px; background-color: #fff3cd; border-radius: 8px; border-left: 4px solid #ffc107;"></div>
  </div>
</div>

<script>
var artworks = {
  {% for item in site.syrian_refugee_art %}
  "{{ item.pid }}": {
    title: {{ item.title | jsonify }},
    artist: {{ item.artist | jsonify }},
    date: {{ item._date | jsonify }},
    description: {{ item.description | jsonify }},
    medium: {{ item.medium | jsonify }},
    location: {{ item.location | jsonify }},
    thumbnail: {{ item.thumbnail | jsonify }},
    url: {{ item.url | jsonify }}
  }{% unless forloop.last %},{% endunless %}
  {% endfor %}
};

function compareArtworks() {
  var pid1 = document.getElementById('compare-artwork-1').value;
  var pid2 = document.getElementById('compare-artwork-2').value;
  
  if (!pid1 || !pid2) {
    alert('Please select two artworks to compare.');
    return;
  }
  
  if (pid1 === pid2) {
    alert('Please select two different artworks.');
    return;
  }
  
  var artwork1 = artworks[pid1];
  var artwork2 = artworks[pid2];
  
  if (!artwork1 || !artwork2) {
    alert('Error loading artwork data.');
    return;
  }
  
  displayComparison(artwork1, artwork2);
  generateInsights(artwork1, artwork2);
  trackAction('compare', pid1 + '_vs_' + pid2, pid1);
}

function displayComparison(artwork1, artwork2) {
  var resultsDiv = document.getElementById('comparison-results');
  var item1Div = document.getElementById('artwork-1-details');
  var item2Div = document.getElementById('artwork-2-details');
  
  item1Div.innerHTML = `
    <h4><a href="${artwork1.url}">${artwork1.title}</a></h4>
    <img src="${artwork1.thumbnail}" alt="${artwork1.title}" style="width: 100%; max-width: 400px; margin: 15px 0; border-radius: 4px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
    <table style="width: 100%; margin-top: 15px;">
      <tr><td style="padding: 5px 0;"><strong>Artist:</strong></td><td style="padding: 5px 0;">${artwork1.artist}</td></tr>
      <tr><td style="padding: 5px 0;"><strong>Date:</strong></td><td style="padding: 5px 0;">${artwork1.date || 'N/A'}</td></tr>
      <tr><td style="padding: 5px 0;"><strong>Medium:</strong></td><td style="padding: 5px 0;">${artwork1.medium || 'N/A'}</td></tr>
      <tr><td style="padding: 5px 0;"><strong>Location:</strong></td><td style="padding: 5px 0;">${artwork1.location || 'N/A'}</td></tr>
    </table>
    <div style="margin-top: 15px;">
      <strong>Description:</strong>
      <p style="margin-top: 5px;">${artwork1.description || 'N/A'}</p>
    </div>
    <a href="${artwork1.url}" style="display: inline-block; margin-top: 15px; padding: 8px 16px; background-color: #0066cc; color: white; text-decoration: none; border-radius: 4px;">View Full Page →</a>
  `;
  
  item2Div.innerHTML = `
    <h4><a href="${artwork2.url}">${artwork2.title}</a></h4>
    <img src="${artwork2.thumbnail}" alt="${artwork2.title}" style="width: 100%; max-width: 400px; margin: 15px 0; border-radius: 4px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
    <table style="width: 100%; margin-top: 15px;">
      <tr><td style="padding: 5px 0;"><strong>Artist:</strong></td><td style="padding: 5px 0;">${artwork2.artist}</td></tr>
      <tr><td style="padding: 5px 0;"><strong>Date:</strong></td><td style="padding: 5px 0;">${artwork2.date || 'N/A'}</td></tr>
      <tr><td style="padding: 5px 0;"><strong>Medium:</strong></td><td style="padding: 5px 0;">${artwork2.medium || 'N/A'}</td></tr>
      <tr><td style="padding: 5px 0;"><strong>Location:</strong></td><td style="padding: 5px 0;">${artwork2.location || 'N/A'}</td></tr>
    </table>
    <div style="margin-top: 15px;">
      <strong>Description:</strong>
      <p style="margin-top: 5px;">${artwork2.description || 'N/A'}</p>
    </div>
    <a href="${artwork2.url}" style="display: inline-block; margin-top: 15px; padding: 8px 16px; background-color: #0066cc; color: white; text-decoration: none; border-radius: 4px;">View Full Page →</a>
  `;
  
  resultsDiv.style.display = 'block';
  resultsDiv.scrollIntoView({ behavior: 'smooth' });
}

function generateInsights(artwork1, artwork2) {
  var insights = [];
  var insightsDiv = document.getElementById('comparison-insights');
  
  // Compare artists
  if (artwork1.artist === artwork2.artist) {
    insights.push(`Both artworks are by <strong>${artwork1.artist}</strong>, showing different perspectives from the same artist.`);
  }
  
  // Compare dates
  if (artwork1.date && artwork2.date) {
    var date1 = parseInt(artwork1.date);
    var date2 = parseInt(artwork2.date);
    if (!isNaN(date1) && !isNaN(date2)) {
      var diff = Math.abs(date1 - date2);
      if (diff <= 2) {
        insights.push(`Both artworks were created within ${diff} year(s) of each other (${artwork1.date} and ${artwork2.date}), reflecting similar historical context.`);
      }
    }
  }
  
  // Compare medium
  if (artwork1.medium && artwork2.medium && artwork1.medium === artwork2.medium) {
    insights.push(`Both artworks use the same medium: <strong>${artwork1.medium}</strong>.`);
  }
  
  // Compare location
  if (artwork1.location && artwork2.location && artwork1.location === artwork2.location) {
    insights.push(`Both artworks are associated with the same location: <strong>${artwork1.location}</strong>.`);
  }
  
  if (insights.length > 0) {
    insightsDiv.innerHTML = '<h5>💡 Comparison Insights</h5><ul style="margin: 10px 0; padding-left: 20px;">' + 
      insights.map(i => '<li style="margin: 5px 0;">' + i + '</li>').join('') + 
      '</ul>';
  } else {
    insightsDiv.innerHTML = '<h5>💡 Comparison Insights</h5><p>These artworks offer different perspectives on the Syrian refugee experience. Compare their themes, styles, and contexts to discover connections.</p>';
  }
}

function clearComparison() {
  document.getElementById('comparison-results').style.display = 'none';
  document.getElementById('compare-artwork-1').value = '';
  document.getElementById('compare-artwork-2').value = '';
}

function trackAction(actionType, actionDetail, artworkId) {
  if (typeof localStorage !== 'undefined') {
    var actions = JSON.parse(localStorage.getItem('syrianRefugeeArtActions') || '{}');
    var key = actionType + '_' + actionDetail;
    actions[key] = (actions[key] || 0) + 1;
    actions['total_' + actionType] = (actions['total_' + actionType] || 0) + 1;
    localStorage.setItem('syrianRefugeeArtActions', JSON.stringify(actions));
    updateImpactCounter();
  }
}

function updateImpactCounter() {
  var actions = JSON.parse(localStorage.getItem('syrianRefugeeArtActions') || '{}');
  var totalComparisons = actions['total_compare'] || 0;
  var counter = document.getElementById('total-comparisons-counter');
  if (counter) {
    counter.textContent = totalComparisons.toLocaleString();
  }
}
</script>

<style>
@media (max-width: 768px) {
  .comparison-grid {
    grid-template-columns: 1fr !important;
  }
  .comparison-controls {
    flex-direction: column;
  }
  .compare-select {
    width: 100% !important;
    margin-bottom: 10px !important;
  }
}
</style>

