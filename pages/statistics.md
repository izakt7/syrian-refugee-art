---
layout: page
title: Statistics & Data
permalink: /statistics/
---

## Syrian Refugee Crisis: Data & Statistics

Explore data visualizations that help contextualize the artworks in this collection. All statistics are sourced from UNHCR and verified humanitarian organizations as of 2024.

<div style="margin: 20px 0; padding: 15px; background-color: #e7f3ff; border-left: 4px solid #0066cc; border-radius: 4px;">
  <strong>📊 Data Sources:</strong> Statistics compiled from <a href="https://www.unhcr.org/" target="_blank">UNHCR</a>, <a href="https://www.unrefugees.org/" target="_blank">USA for UNHCR</a>, and other verified humanitarian organizations. Last updated: December 2024. <a href="{{ '/sources/' | absolute_url }}">View all sources →</a>
</div>

### Scale of Displacement

<div class="stat-visualization" style="margin: 30px 0; padding: 20px; background-color: #f8f9fa; border-radius: 8px;">
  <h4>Syrian Refugees by Host Country</h4>
  <div class="bar-chart" style="margin: 20px 0;">
    <div class="bar-item" style="margin: 10px 0;">
      <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
        <span><strong>Turkey</strong></span>
        <span>3.6 million</span>
      </div>
      <div style="width: 100%; background-color: #e9ecef; border-radius: 5px; height: 30px; overflow: hidden;">
        <div style="height: 100%; background: linear-gradient(90deg, #667eea 0%, #764ba2 100%); width: 100%; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold;">
          3.6M
        </div>
      </div>
    </div>
    
    <div class="bar-item" style="margin: 10px 0;">
      <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
        <span><strong>Lebanon</strong></span>
        <span>1.5 million</span>
      </div>
      <div style="width: 100%; background-color: #e9ecef; border-radius: 5px; height: 30px; overflow: hidden;">
        <div style="height: 100%; background: linear-gradient(90deg, #f093fb 0%, #f5576c 100%); width: 42%; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold;">
          1.5M
        </div>
      </div>
    </div>
    
    <div class="bar-item" style="margin: 10px 0;">
      <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
        <span><strong>Jordan</strong></span>
        <span>1.3 million</span>
      </div>
      <div style="width: 100%; background-color: #e9ecef; border-radius: 5px; height: 30px; overflow: hidden;">
        <div style="height: 100%; background: linear-gradient(90deg, #4facfe 0%, #00f2fe 100%); width: 36%; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold;">
          1.3M
        </div>
      </div>
    </div>
    
    <div class="bar-item" style="margin: 10px 0;">
      <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
        <span><strong>Germany</strong></span>
        <span>800,000+</span>
      </div>
      <div style="width: 100%; background-color: #e9ecef; border-radius: 5px; height: 30px; overflow: hidden;">
        <div style="height: 100%; background: linear-gradient(90deg, #43e97b 0%, #38f9d7 100%); width: 22%; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold;">
          800K+
        </div>
      </div>
    </div>
    
    <div class="bar-item" style="margin: 10px 0;">
      <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
        <span><strong>Iraq</strong></span>
        <span>250,000</span>
      </div>
      <div style="width: 100%; background-color: #e9ecef; border-radius: 5px; height: 30px; overflow: hidden;">
        <div style="height: 100%; background: linear-gradient(90deg, #fa709a 0%, #fee140 100%); width: 7%; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold;">
          250K
        </div>
      </div>
    </div>
  </div>
</div>

### Collection Statistics

<div class="collection-stats" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; margin: 30px 0;">
  <div class="stat-box" style="padding: 20px; background-color: #fff; border: 2px solid #dee2e6; border-radius: 8px; text-align: center;">
    <div style="font-size: 2.5em; font-weight: bold; color: #0066cc;">11</div>
    <div style="margin-top: 10px; color: #6c757d;">Total Items</div>
  </div>
  
  <div class="stat-box" style="padding: 20px; background-color: #fff; border: 2px solid #dee2e6; border-radius: 8px; text-align: center;">
    <div style="font-size: 2.5em; font-weight: bold; color: #0066cc;">10</div>
    <div style="margin-top: 10px; color: #6c757d;">Artworks</div>
  </div>
  
  <div class="stat-box" style="padding: 20px; background-color: #fff; border: 2px solid #dee2e6; border-radius: 8px; text-align: center;">
    <div style="font-size: 2.5em; font-weight: bold; color: #0066cc;">1</div>
    <div style="margin-top: 10px; color: #6c757d;">Video</div>
  </div>
  
  <div class="stat-box" style="padding: 20px; background-color: #fff; border: 2px solid #dee2e6; border-radius: 8px; text-align: center;">
    <div style="font-size: 2.5em; font-weight: bold; color: #0066cc;">5</div>
    <div style="margin-top: 10px; color: #6c757d;">Unique Artists</div>
  </div>
</div>

### Artworks by Year

<div class="timeline-chart" style="margin: 30px 0; padding: 20px; background-color: #f8f9fa; border-radius: 8px;">
  <h4>Artworks Created Over Time</h4>
  <div style="margin-top: 20px;">
    {% assign years = "2016,2017,2018" | split: "," %}
    {% for year in years %}
      {% assign year_count = 0 %}
      {% for item in site.syrian_refugee_art %}
        {% assign item_year = item._date | plus: 0 %}
        {% if item_year == year | plus: 0 %}
          {% assign year_count = year_count | plus: 1 %}
        {% endif %}
      {% endfor %}
      {% if year_count > 0 %}
        <div style="margin: 15px 0;">
          <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
            <span><strong>{{ year }}</strong></span>
            <span>{{ year_count }} artwork{{ year_count | pluralize: '', 's' }}</span>
          </div>
          <div style="width: 100%; background-color: #e9ecef; border-radius: 5px; height: 25px; overflow: hidden;">
            <div style="height: 100%; background: linear-gradient(90deg, #667eea 0%, #764ba2 100%); width: {{ year_count | times: 20 }}%; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold; font-size: 0.9em;">
              {{ year_count }}
            </div>
          </div>
        </div>
      {% endif %}
    {% endfor %}
  </div>
</div>

### Artworks by Medium

<div class="medium-chart" style="margin: 30px 0; padding: 20px; background-color: #f8f9fa; border-radius: 8px;">
  <h4>Distribution by Medium</h4>
  <div style="margin-top: 20px;">
    {% assign mediums = site.syrian_refugee_art | map: 'medium' | uniq | compact %}
    {% for medium in mediums %}
      {% assign medium_count = 0 %}
      {% for item in site.syrian_refugee_art %}
        {% if item.medium == medium %}
          {% assign medium_count = medium_count | plus: 1 %}
        {% endif %}
      {% endfor %}
      {% if medium_count > 0 %}
        <div style="margin: 10px 0;">
          <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
            <span>{{ medium }}</span>
            <span>{{ medium_count }}</span>
          </div>
          <div style="width: 100%; background-color: #e9ecef; border-radius: 5px; height: 20px; overflow: hidden;">
            <div style="height: 100%; background: linear-gradient(90deg, #4facfe 0%, #00f2fe 100%); width: {{ medium_count | times: 10 }}%;"></div>
          </div>
        </div>
      {% endif %}
    {% endfor %}
  </div>
</div>

### Key Statistics

<div class="key-stats" style="margin: 30px 0; padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border-radius: 8px;">
  <h4 style="color: white; margin-bottom: 15px;">The Crisis in Numbers (2024)</h4>
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px;">
    <div>
      <div style="font-size: 2em; font-weight: bold;">13.4 Million</div>
      <div style="margin-top: 5px; opacity: 0.9;">Total Syrians Displaced</div>
      <div style="margin-top: 5px; font-size: 0.85em; opacity: 0.8;">6.1M refugees + 7.4M internally displaced</div>
    </div>
    <div>
      <div style="font-size: 2em; font-weight: bold;">50%</div>
      <div style="margin-top: 5px; opacity: 0.9;">Are Children</div>
      <div style="margin-top: 5px; font-size: 0.85em; opacity: 0.8;">Over 3 million child refugees</div>
    </div>
    <div>
      <div style="font-size: 2em; font-weight: bold;">85%</div>
      <div style="margin-top: 5px; opacity: 0.9;">In Neighboring Countries</div>
      <div style="margin-top: 5px; font-size: 0.85em; opacity: 0.8;">Turkey, Lebanon, Jordan, Iraq</div>
    </div>
    <div>
      <div style="font-size: 2em; font-weight: bold;">13+ Years</div>
      <div style="margin-top: 5px; opacity: 0.9;">Since Conflict Began (2011)</div>
      <div style="margin-top: 5px; font-size: 0.85em; opacity: 0.8;">One of the longest conflicts</div>
    </div>
  </div>
</div>

### Additional Statistics

<div class="additional-stats" style="margin: 30px 0; padding: 20px; background-color: #f8f9fa; border-radius: 8px;">
  <h4>More Key Facts</h4>
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-top: 15px;">
    <div>
      <strong>6.1 Million</strong> Syrian refugees and asylum-seekers worldwide (UNHCR, 2024)
    </div>
    <div>
      <strong>7.4 Million</strong> Internally displaced persons within Syria (UNHCR, 2024)
    </div>
    <div>
      <strong>580,000+</strong> Estimated deaths since conflict began (as of 2022)
    </div>
    <div>
      <strong>90%</strong> Of Syrian refugees live below the poverty line in host countries
    </div>
    <div>
      <strong>1.5 Million</strong> Syrian children born as refugees since 2011
    </div>
    <div>
      <strong>2.5 Million</strong> Syrian children out of school
    </div>
  </div>
</div>

---

### Sources

All statistics are sourced from verified humanitarian organizations. For complete citations and references, see our [Sources page]({{ '/sources/' | absolute_url }}).

---

[← Back to Home]({{ '/' | absolute_url }})

