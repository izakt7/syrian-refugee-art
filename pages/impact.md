---
layout: page
title: Our Impact
permalink: /impact/
---

## Community Impact

See how visitors to this exhibition are taking action to support Syrian refugees.

<div class="impact-dashboard" style="margin: 30px 0;">
  <div class="impact-stats" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; margin-bottom: 30px;">
    <div class="stat-card" style="padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border-radius: 8px; text-align: center;">
      <div class="stat-number" id="total-shares-counter" style="font-size: 2.5em; font-weight: bold; margin-bottom: 10px;">0</div>
      <div class="stat-label" style="font-size: 1.1em;">Artworks Shared</div>
    </div>
    
    <div class="stat-card" style="padding: 20px; background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; border-radius: 8px; text-align: center;">
      <div class="stat-number" id="total-comparisons-counter" style="font-size: 2.5em; font-weight: bold; margin-bottom: 10px;">0</div>
      <div class="stat-label" style="font-size: 1.1em;">Artworks Compared</div>
    </div>
    
    <div class="stat-card" style="padding: 20px; background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); color: white; border-radius: 8px; text-align: center;">
      <div class="stat-number" id="total-actions-counter" style="font-size: 2.5em; font-weight: bold; margin-bottom: 10px;">0</div>
      <div class="stat-label" style="font-size: 1.1em;">Total Actions Taken</div>
    </div>
    
    <div class="stat-card" style="padding: 20px; background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%); color: white; border-radius: 8px; text-align: center;">
      <div class="stat-number" style="font-size: 2.5em; font-weight: bold; margin-bottom: 10px;">11</div>
      <div class="stat-label" style="font-size: 1.1em;">Artworks in Collection</div>
    </div>
  </div>
  
  <div class="impact-progress" style="margin: 30px 0;">
    <h3>Community Engagement Goals</h3>
    
    <div class="progress-item" style="margin: 20px 0;">
      <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
        <span><strong>Share 1,000 Artworks</strong></span>
        <span id="shares-progress-text">0 / 1,000</span>
      </div>
      <div style="width: 100%; background-color: #e9ecef; border-radius: 10px; height: 25px; overflow: hidden;">
        <div id="shares-progress-bar" style="height: 100%; background: linear-gradient(90deg, #667eea 0%, #764ba2 100%); width: 0%; transition: width 0.3s; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold; font-size: 0.8em;">
        </div>
      </div>
    </div>
    
    <div class="progress-item" style="margin: 20px 0;">
      <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
        <span><strong>Compare 500 Artwork Pairs</strong></span>
        <span id="comparisons-progress-text">0 / 500</span>
      </div>
      <div style="width: 100%; background-color: #e9ecef; border-radius: 10px; height: 25px; overflow: hidden;">
        <div id="comparisons-progress-bar" style="height: 100%; background: linear-gradient(90deg, #f093fb 0%, #f5576c 100%); width: 0%; transition: width 0.3s; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold; font-size: 0.8em;">
        </div>
      </div>
    </div>
  </div>
  
  <div class="impact-stories" style="margin: 30px 0; padding: 20px; background-color: #f8f9fa; border-radius: 8px;">
    <h3>How This Exhibition Creates Impact</h3>
    <ul style="line-height: 1.8;">
      <li><strong>Raising Awareness:</strong> Each share helps spread awareness about the Syrian refugee crisis</li>
      <li><strong>Building Empathy:</strong> Comparing artworks helps visitors understand different perspectives</li>
      <li><strong>Inspiring Action:</strong> Learning about the crisis motivates visitors to donate, volunteer, or advocate</li>
      <li><strong>Preserving Stories:</strong> Documenting and sharing refugee art preserves important cultural heritage</li>
      <li><strong>Creating Connections:</strong> Building understanding between refugees and host communities</li>
    </ul>
  </div>
</div>

<script>
function updateImpactCounters() {
  var actions = JSON.parse(localStorage.getItem('syrianRefugeeArtActions') || '{}');
  
  // Update counters
  var totalShares = actions['total_share'] || 0;
  var totalComparisons = actions['total_compare'] || 0;
  var totalActions = totalShares + totalComparisons;
  
  document.getElementById('total-shares-counter').textContent = totalShares.toLocaleString();
  document.getElementById('total-comparisons-counter').textContent = totalComparisons.toLocaleString();
  document.getElementById('total-actions-counter').textContent = totalActions.toLocaleString();
  
  // Update progress bars
  var sharesGoal = 1000;
  var comparisonsGoal = 500;
  
  var sharesPercent = Math.min((totalShares / sharesGoal) * 100, 100);
  var comparisonsPercent = Math.min((totalComparisons / comparisonsGoal) * 100, 100);
  
  document.getElementById('shares-progress-bar').style.width = sharesPercent + '%';
  document.getElementById('shares-progress-bar').textContent = Math.round(sharesPercent) + '%';
  document.getElementById('shares-progress-text').textContent = totalShares + ' / ' + sharesGoal;
  
  document.getElementById('comparisons-progress-bar').style.width = comparisonsPercent + '%';
  document.getElementById('comparisons-progress-bar').textContent = Math.round(comparisonsPercent) + '%';
  document.getElementById('comparisons-progress-text').textContent = totalComparisons + ' / ' + comparisonsGoal;
}

document.addEventListener('DOMContentLoaded', function() {
  updateImpactCounters();
  // Update every 5 seconds in case of multiple tabs
  setInterval(updateImpactCounters, 5000);
});
</script>

---

[← Back to Home](/)

