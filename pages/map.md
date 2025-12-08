---
layout: page
title: Interactive Map
permalink: /map/
---

## Geographic Context: Syrian Refugee Art

Explore the geographic locations associated with the artworks and understand the migration patterns of Syrian refugees.

<div id="refugee-map" style="width: 100%; height: 600px; margin: 30px 0; border: 2px solid #dee2e6; border-radius: 8px; background-color: #f8f9fa;">
  <div style="padding: 20px; text-align: center; color: #6c757d;">
    <p>Loading interactive map...</p>
  </div>
</div>

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Initialize map
  var map = L.map('refugee-map').setView([35.0, 38.0], 6);
  
  // Add OpenStreetMap tiles
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
    maxZoom: 18
  }).addTo(map);
  
  // Define locations with coordinates
  var locations = {
    'Syria': { lat: 34.8021, lng: 38.9968, type: 'origin', count: '13.4M displaced' },
    'Turkey': { lat: 39.9334, lng: 32.8597, type: 'host', count: '3.6M refugees' },
    'Lebanon': { lat: 33.8547, lng: 35.8623, type: 'host', count: '1.5M refugees' },
    'Jordan': { lat: 31.9539, lng: 35.9106, type: 'host', count: '1.3M refugees' },
    'Germany': { lat: 51.1657, lng: 10.4515, type: 'host', count: '800K+ refugees' },
    'Iraq': { lat: 33.2232, lng: 43.6793, type: 'host', count: '250K refugees' }
  };
  
  // Get artwork locations from collection
  var artworkLocations = {};
  {% for item in site.syrian_refugee_art %}
    {% if item.location %}
      var loc = {{ item.location | jsonify }};
      if (!artworkLocations[loc]) {
        artworkLocations[loc] = [];
      }
      artworkLocations[loc].push({
        title: {{ item.title | jsonify }},
        url: '{{ item.url | absolute_url }}',
        thumbnail: '{{ item.thumbnail | absolute_url }}'
      });
    {% endif %}
  {% endfor %}
  
  // Add markers
  Object.keys(locations).forEach(function(name) {
    var loc = locations[name];
    var color = loc.type === 'origin' ? '#dc3545' : '#0066cc';
    var icon = L.divIcon({
      className: 'custom-marker',
      html: `<div style="background-color: ${color}; width: 20px; height: 20px; border-radius: 50%; border: 3px solid white; box-shadow: 0 2px 8px rgba(0,0,0,0.3);"></div>`,
      iconSize: [20, 20],
      iconAnchor: [10, 10]
    });
    
    var popupContent = `<strong>${name}</strong><br>${loc.count}`;
    if (artworkLocations[name]) {
      popupContent += '<br><br><strong>Artworks:</strong><ul style="margin: 5px 0; padding-left: 20px;">';
      artworkLocations[name].forEach(function(artwork) {
        popupContent += `<li><a href="${artwork.url}">${artwork.title}</a></li>`;
      });
      popupContent += '</ul>';
    }
    
    L.marker([loc.lat, loc.lng], { icon: icon })
      .addTo(map)
      .bindPopup(popupContent);
  });
  
  // Add migration route lines
  var routes = [
    { from: locations['Syria'], to: locations['Turkey'], color: '#28a745' },
    { from: locations['Syria'], to: locations['Lebanon'], color: '#28a745' },
    { from: locations['Syria'], to: locations['Jordan'], color: '#28a745' },
    { from: locations['Syria'], to: locations['Germany'], color: '#28a745' }
  ];
  
  routes.forEach(function(route) {
    L.polyline(
      [[route.from.lat, route.from.lng], [route.to.lat, route.to.lng]],
      { color: route.color, weight: 2, opacity: 0.6, dashArray: '5, 5' }
    ).addTo(map);
  });
});
</script>

<div class="map-legend" style="margin: 20px 0; padding: 15px; background-color: #f8f9fa; border-radius: 8px;">
  <h4>Map Legend</h4>
  <div style="display: flex; flex-wrap: wrap; gap: 20px; margin-top: 10px;">
    <div style="display: flex; align-items: center;">
      <div style="width: 20px; height: 20px; background-color: #dc3545; border-radius: 50%; margin-right: 8px;"></div>
      <span>Syria (Origin)</span>
    </div>
    <div style="display: flex; align-items: center;">
      <div style="width: 20px; height: 20px; background-color: #0066cc; border-radius: 50%; margin-right: 8px;"></div>
      <span>Refugee Host Country</span>
    </div>
    <div style="display: flex; align-items: center;">
      <div style="width: 40px; height: 2px; background-color: #28a745; margin-right: 8px; border-top: 2px dashed #28a745;"></div>
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
    <p><strong>Syria → Turkey:</strong> Over 3.6 million refugees (largest host country)</p>
    <p><strong>Syria → Lebanon:</strong> Over 1.5 million refugees (highest per capita)</p>
    <p><strong>Syria → Jordan:</strong> Over 1.3 million refugees</p>
    <p><strong>Syria → Europe:</strong> Hundreds of thousands via dangerous sea crossings</p>
    <p><strong>Syria → Germany:</strong> Over 800,000 refugees</p>
    <p><strong>Syria → Iraq:</strong> Over 250,000 refugees</p>
  </div>
  <p style="margin-top: 15px; font-size: 0.9em; color: #6c757d;">
    <em>Source: <a href="https://www.unhcr.org/" target="_blank">UNHCR</a> (2024)</em>
  </p>
</div>

<style>
.location-item:hover {
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transform: translateX(5px);
  transition: all 0.2s;
}

.custom-marker {
  background: transparent !important;
  border: none !important;
}
</style>

---

[← Back to Home](/)
