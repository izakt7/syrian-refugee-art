---
layout: page
title: Interactive Map
permalink: /map/
---

## Geographic Context: Syrian Refugee Art

Explore the geographic locations associated with the artworks and understand the migration patterns of Syrian refugees.

<div id="refugee-map" style="width: 100%; height: 600px; margin: 30px 0; border: 2px solid #dee2e6; border-radius: 8px; background-color: #f8f9fa;">
  <div style="padding: 20px; text-align: center; color: #6c757d;">
    <p>Interactive map loading...</p>
    <p style="font-size: 0.9em; margin-top: 10px;">This map shows locations associated with artworks and major refugee host countries.</p>
  </div>
</div>

<div class="map-legend" style="margin: 20px 0; padding: 15px; background-color: #f8f9fa; border-radius: 8px;">
  <h4>Map Legend</h4>
  <div style="display: flex; flex-wrap: wrap; gap: 20px; margin-top: 10px;">
    <div style="display: flex; align-items: center;">
      <div style="width: 20px; height: 20px; background-color: #dc3545; border-radius: 50%; margin-right: 8px;"></div>
      <span>Artwork Location</span>
    </div>
    <div style="display: flex; align-items: center;">
      <div style="width: 20px; height: 20px; background-color: #0066cc; border-radius: 50%; margin-right: 8px;"></div>
      <span>Major Refugee Host Country</span>
    </div>
    <div style="display: flex; align-items: center;">
      <div style="width: 20px; height: 20px; background-color: #28a745; border-radius: 50%; margin-right: 8px;"></div>
      <span>Migration Route</span>
    </div>
  </div>
</div>

### Locations in the Collection

<div class="location-list" style="margin: 30px 0;">
  {% assign locations = site.syrian_refugee_art | map: 'location' | uniq | compact %}
  {% for location in locations %}
    {% assign location_count = 0 %}
    {% assign location_artworks = '' %}
    {% for item in site.syrian_refugee_art %}
      {% if item.location == location %}
        {% assign location_count = location_count | plus: 1 %}
        {% if location_artworks == '' %}
          {% assign location_artworks = item.title %}
        {% else %}
          {% assign location_artworks = location_artworks | append: ', ' | append: item.title %}
        {% endif %}
      {% endif %}
    {% endfor %}
    {% if location_count > 0 %}
      <div class="location-item" style="padding: 15px; margin: 10px 0; background-color: #fff; border-left: 4px solid #0066cc; border-radius: 4px;">
        <h5 style="margin: 0 0 5px 0;">📍 {{ location }}</h5>
        <p style="margin: 0; color: #6c757d; font-size: 0.9em;">
          {{ location_count }} artwork{{ location_count | pluralize: '', 's' }}: {{ location_artworks }}
        </p>
      </div>
    {% endif %}
  {% endfor %}
</div>

### Migration Routes

<div class="migration-routes" style="margin: 30px 0; padding: 20px; background-color: #f8f9fa; border-radius: 8px;">
  <h4>Common Migration Routes</h4>
  <div style="margin-top: 15px; line-height: 2;">
    <p><strong>Syria → Turkey:</strong> Over 3.6 million refugees</p>
    <p><strong>Syria → Lebanon:</strong> Over 1.5 million refugees</p>
    <p><strong>Syria → Jordan:</strong> Over 1.3 million refugees</p>
    <p><strong>Syria → Europe:</strong> Hundreds of thousands via dangerous sea crossings</p>
    <p><strong>Syria → Germany:</strong> Over 800,000 refugees</p>
  </div>
</div>

<script>
// Simple map visualization using CSS and HTML
// For a full interactive map, you would integrate Leaflet.js or Google Maps

document.addEventListener('DOMContentLoaded', function() {
  var mapContainer = document.getElementById('refugee-map');
  
  // Create a simple visual representation
  mapContainer.innerHTML = `
    <div style="position: relative; width: 100%; height: 100%; background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%); border-radius: 6px; overflow: hidden;">
      <div style="position: absolute; top: 20%; left: 60%; width: 15px; height: 15px; background-color: #dc3545; border-radius: 50%; border: 3px solid white; box-shadow: 0 2px 8px rgba(0,0,0,0.3);" title="Syria"></div>
      <div style="position: absolute; top: 15%; left: 65%; width: 20px; height: 20px; background-color: #0066cc; border-radius: 50%; border: 3px solid white; box-shadow: 0 2px 8px rgba(0,0,0,0.3);" title="Turkey - 3.6M refugees"></div>
      <div style="position: absolute; top: 35%; left: 60%; width: 18px; height: 18px; background-color: #0066cc; border-radius: 50%; border: 3px solid white; box-shadow: 0 2px 8px rgba(0,0,0,0.3);" title="Lebanon - 1.5M refugees"></div>
      <div style="position: absolute; top: 40%; left: 65%; width: 17px; height: 17px; background-color: #0066cc; border-radius: 50%; border: 3px solid white; box-shadow: 0 2px 8px rgba(0,0,0,0.3);" title="Jordan - 1.3M refugees"></div>
      <div style="position: absolute; top: 10%; left: 25%; width: 16px; height: 16px; background-color: #0066cc; border-radius: 50%; border: 3px solid white; box-shadow: 0 2px 8px rgba(0,0,0,0.3);" title="Germany - 800K+ refugees"></div>
      
      <!-- Migration route lines -->
      <svg style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none;">
        <line x1="60%" y1="20%" x2="65%" y2="15%" stroke="#28a745" stroke-width="2" stroke-dasharray="5,5" opacity="0.6"></line>
        <line x1="60%" y1="20%" x2="60%" y2="35%" stroke="#28a745" stroke-width="2" stroke-dasharray="5,5" opacity="0.6"></line>
        <line x1="60%" y1="20%" x2="65%" y2="40%" stroke="#28a745" stroke-width="2" stroke-dasharray="5,5" opacity="0.6"></line>
        <line x1="60%" y1="20%" x2="25%" y2="10%" stroke="#28a745" stroke-width="2" stroke-dasharray="5,5" opacity="0.6"></line>
      </svg>
      
      <div style="position: absolute; bottom: 20px; left: 20px; background-color: white; padding: 15px; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2); max-width: 300px;">
        <h5 style="margin: 0 0 10px 0;">Migration Overview</h5>
        <p style="margin: 0; font-size: 0.9em; color: #6c757d;">
          Click on locations to see associated artworks. The dashed lines show common migration routes from Syria.
        </p>
      </div>
    </div>
  `;
  
  // Add click handlers for locations
  var locations = [
    { name: 'Syria', artworks: ['Multiple artworks'] },
    { name: 'Turkey', artworks: ['artwork2'] },
    { name: 'Lebanon', artworks: ['artwork3', 'artwork6', 'artwork7', 'artwork8'] },
    { name: 'Jordan', artworks: ['artwork7'] },
    { name: 'Germany', artworks: ['artwork5'] }
  ];
});
</script>

<style>
.location-item:hover {
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transform: translateX(5px);
  transition: all 0.2s;
}
</style>

---

[← Back to Home](/)

