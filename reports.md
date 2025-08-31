---
layout: default
title: "Stock Research Reports - Nivest India"
description: "Browse all stock research reports with comprehensive analysis and investment recommendations for Indian markets"
permalink: /reports/
---

<div class="page-header">
  <h1>Stock Research Reports</h1>
  <p>Comprehensive stock research reports with AI-powered analysis, detailed financial modeling, and actionable investment recommendations for Indian markets.</p>
</div>

## Browse All Reports

<div class="search-container">
  <div class="search-header">
    <span class="search-icon">🔍</span>
    <h3 class="search-title">Search Stock Research Reports</h3>
  </div>
  <input type="text" id="stock-search" placeholder="Enter company name, ticker symbol, or sector to filter results..." />
  <div class="search-results-info">
    <span id="results-count"></span>
  </div>
</div>

<div id="search-results">
{% for post in site.posts %}
<div class="research-summary" data-title="{{ post.title | downcase }}" data-ticker="{{ post.ticker | downcase }}" data-sector="{{ post.sector | downcase }}">
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
  <p><strong>Ticker:</strong> {{ post.ticker }} | <strong>Sector:</strong> {{ post.sector }}</p>
  <p><strong>Current Price:</strong> {{ post.current_price }} | <strong>Market Cap:</strong> {{ post.market_cap }}</p>
  <p><strong>Recommendation:</strong> <span class="recommendation {{ post.recommendation | downcase }}">{{ post.recommendation }}</span> | <strong>Strategy:</strong> {{ post.strategy_type }} | <strong>Target:</strong> {{ post.target_price }}</p>
  <p><em>Published: {{ post.date | date: "%B %d, %Y" }}</em></p>
</div>
{% endfor %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
    const searchInput = document.getElementById('stock-search');
    const resultsContainer = document.getElementById('search-results');
    const resultsCount = document.getElementById('results-count');
    const allItems = document.querySelectorAll('.research-summary');
    
    // Initialize results count
    updateResultsCount(allItems.length);
    
    // Search functionality with debounce for better performance
    let searchTimeout;
    searchInput.addEventListener('input', function() {
        const searchTerm = this.value.toLowerCase().trim();
        
        // Add active class for visual feedback
        if (searchTerm !== '') {
            this.classList.add('searching');
        } else {
            this.classList.remove('searching');
        }
        
        // Clear previous timeout
        clearTimeout(searchTimeout);
        
        // Debounce search for better performance
        searchTimeout = setTimeout(() => {
            if (searchTerm === '') {
                // Show all items
                allItems.forEach(item => {
                    item.classList.remove('hidden');
                });
                updateResultsCount(allItems.length);
            } else {
                let visibleCount = 0;
                
                allItems.forEach(item => {
                    const title = item.getAttribute('data-title') || '';
                    const ticker = item.getAttribute('data-ticker') || '';
                    const sector = item.getAttribute('data-sector') || '';
                    
                    // Check if search term matches title, ticker, or sector
                    if (title.includes(searchTerm) || 
                        ticker.includes(searchTerm) || 
                        sector.includes(searchTerm)) {
                        item.classList.remove('hidden');
                        visibleCount++;
                    } else {
                        item.classList.add('hidden');
                    }
                });
                
                updateResultsCount(visibleCount);
            }
        }, 150); // Small delay for better performance
    });
    
    function updateResultsCount(count) {
        if (count === 0) {
            resultsCount.textContent = 'No stocks found';
        } else if (count === 1) {
            resultsCount.textContent = '1 stock found';
        } else {
            resultsCount.textContent = count + ' stocks found';
        }
    }
    
    // Add keyboard navigation
    searchInput.addEventListener('keydown', function(e) {
        if (e.key === 'Escape') {
            this.value = '';
            this.dispatchEvent(new Event('input'));
            this.blur();
        }
    });
});
</script>
