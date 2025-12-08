---
layout: page
show_title: false
banner:
  collection: syrian_refugee_art
  pid: artwork1
  y: 25%
  clickable: yes
  height: '500px'
---

Since 2011, Syria has been engulfed in a devastating civil war that has resulted in one of the largest humanitarian crises of our time. Over 13 million Syrians have been displaced—more than half of the country's pre-war population—with millions seeking refuge in neighboring countries and beyond. The conflict has destroyed cities, separated families, and created a generation of children who have known nothing but war and displacement. In refugee camps across Jordan, Lebanon, Turkey, and beyond, Syrian families struggle to rebuild their lives while preserving their culture, memories, and hope for the future.

This exhibition brings together artworks created by Syrian artists and refugees who have used their creative expression to document, process, and share their experiences. These works serve as powerful testimonies to human resilience, bearing witness to the trauma of displacement while also celebrating the enduring spirit of the Syrian people. Through paintings, photographs, installations, and multimedia works, these artists transform personal and collective suffering into art that demands our attention, empathy, and action. By engaging with these artworks, we not only honor the stories they tell but also recognize our shared responsibility to support those who have been forced to flee their homes.

### Take Action

<div class="cta-buttons" style="display: flex; flex-wrap: wrap; gap: 15px; margin: 30px 0; justify-content: center;">
  <a href="/donate/" class="btn btn-primary" style="padding: 12px 24px; background-color: #0066cc; color: white; text-decoration: none; border-radius: 5px; font-weight: bold; display: inline-block;">Donate / Volunteer</a>
  <a href="/fact-check/" class="btn btn-secondary" style="padding: 12px 24px; background-color: #28a745; color: white; text-decoration: none; border-radius: 5px; font-weight: bold; display: inline-block;">Share Responsibility (Fact Check Card)</a>
  <a href="/contact-rep/" class="btn btn-tertiary" style="padding: 12px 24px; background-color: #dc3545; color: white; text-decoration: none; border-radius: 5px; font-weight: bold; display: inline-block;">Message Your Rep</a>
</div>

<div class="impact-counter-home" style="margin: 30px 0; padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border-radius: 8px; text-align: center;">
  <h4 style="color: white; margin-bottom: 10px;">Community Impact</h4>
  <div style="font-size: 2em; font-weight: bold; margin-bottom: 5px;" id="home-total-actions">0</div>
  <div style="opacity: 0.9;">actions taken by visitors</div>
  <a href="/impact/" style="display: inline-block; margin-top: 15px; padding: 8px 16px; background-color: white; color: #667eea; text-decoration: none; border-radius: 4px; font-weight: bold;">View Impact Dashboard →</a>
</div>

<script>
function updateHomeImpactCounter() {
  if (typeof localStorage !== 'undefined') {
    var actions = JSON.parse(localStorage.getItem('syrianRefugeeArtActions') || '{}');
    var totalShares = actions['total_share'] || 0;
    var totalComparisons = actions['total_compare'] || 0;
    var totalActions = totalShares + totalComparisons;
    var counter = document.getElementById('home-total-actions');
    if (counter) {
      counter.textContent = totalActions.toLocaleString();
    }
  }
}
document.addEventListener('DOMContentLoaded', updateHomeImpactCounter);
setInterval(updateHomeImpactCounter, 5000);
</script>

### Explore the Collection

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px; margin: 30px 0;">
  <a href="/collection/" style="padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; text-decoration: none; border-radius: 8px; text-align: center;">
    <div style="font-size: 2em; margin-bottom: 10px;">🖼️</div>
    <div style="font-weight: bold; font-size: 1.1em;">Browse Collection</div>
    <div style="font-size: 0.9em; margin-top: 5px; opacity: 0.9;">View all artworks</div>
  </a>
  
  <a href="/compare/" style="padding: 20px; background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; text-decoration: none; border-radius: 8px; text-align: center;">
    <div style="font-size: 2em; margin-bottom: 10px;">⚖️</div>
    <div style="font-weight: bold; font-size: 1.1em;">Compare Artworks</div>
    <div style="font-size: 0.9em; margin-top: 5px; opacity: 0.9;">Side-by-side comparison</div>
  </a>
  
  <a href="/map/" style="padding: 20px; background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); color: white; text-decoration: none; border-radius: 8px; text-align: center;">
    <div style="font-size: 2em; margin-bottom: 10px;">🗺️</div>
    <div style="font-weight: bold; font-size: 1.1em;">Interactive Map</div>
    <div style="font-size: 0.9em; margin-top: 5px; opacity: 0.9;">Geographic context</div>
  </a>
  
  <a href="/statistics/" style="padding: 20px; background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%); color: white; text-decoration: none; border-radius: 8px; text-align: center;">
    <div style="font-size: 2em; margin-bottom: 10px;">📊</div>
    <div style="font-weight: bold; font-size: 1.1em;">Statistics</div>
    <div style="font-size: 0.9em; margin-top: 5px; opacity: 0.9;">Data & insights</div>
  </a>
</div>

#### By Medium
{% include collection_gallery_custom.html facet_by='medium' collection='syrian_refugee_art' %}
