---
layout: default
title: State of JS 2027
---

# Survey Results

{% for category in site.data.results %}
<section class="category">
  <h2>{{ category.title }}</h2>
  <canvas id="chart-{{ category.id }}" width="400" height="200"></canvas>
</section>
{% endfor %}

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
  {% for category in site.data.results %}
    const ctx{{ category.id }} = document.getElementById('chart-{{ category.id }}').getContext('2d');
    new Chart(ctx{{ category.id }}, {
      type: 'bar',
      data: {
        labels: [{% for item in category.items %}"{{ item.name }}",{% endfor %}],
        datasets: [{
          label: 'Satisfaction (%)',
          data: [{% for item in category.items %}{{ item.satisfaction }},{% endfor %}],
          backgroundColor: '#3e95cd'
        }]
      }
    });
  {% endfor %}
</script>
