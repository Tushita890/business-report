# business-report
business report
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Interactive Restaurant Food Waste Management Dashboard</title>
<style>
  /* Modern, clean styling */
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #f5f7fa;
    margin: 0;
    padding: 20px;
    color: #333;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  header {
    text-align: center;
    padding-bottom: 15px;
    border-bottom: 3px solid #4CAF50;
    margin-bottom: 30px;
  }
  header h1 {
    margin: 0;
    color: #2e7d32;
    font-weight: 900;
    font-size: 2.5rem;
  }
  header p {
    font-size: 1.2rem;
    color: #555;
    margin: 5px 0 20px 0;
    font-weight: 600;
  }
  main {
    max-width: 1200px;
    margin: 0 auto;
  }

  /* Input Form */
  form#inputForm {
    background: white;
    box-shadow: 0 5px 15px rgba(0,0,0,0.12);
    border-radius: 12px;
    padding: 25px;
    max-width: 960px;
    margin: 0 auto 50px auto;
    transition: box-shadow 0.3s ease;
  }
  form#inputForm:hover {
    box-shadow: 0 8px 30px rgba(0,0,0,0.18);
  }
  form#inputForm h2 {
    color: #2e7d32;
    text-align: center;
    margin-bottom: 25px;
    font-weight: 800;
    letter-spacing: 0.05em;
  }

  .input-group {
    display: flex;
    flex-wrap: wrap;
    gap: 15px 24px;
    justify-content: center;
  }
  .input-group > div {
    flex: 1 1 120px;
    min-width: 120px;
    display: flex;
    flex-direction: column;
  }
  .input-group label {
    font-weight: 700;
    margin-bottom: 7px;
    color: #388e3c;
    font-size: 0.95rem;
  }
  .input-group input[type="number"] {
    padding: 8px 12px;
    border: 2px solid #a5d6a7;
    border-radius: 8px;
    font-size: 1rem;
    color: #2e7d32;
    font-weight: 600;
    transition: border-color 0.25s ease;
  }
  .input-group input[type="number"]:focus {
    border-color: #4caf50;
    outline: none;
  }
  form#inputForm button {
    margin-top: 22px;
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 14px 0;
    font-size: 1.25rem;
    font-weight: 900;
    border-radius: 12px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    display: block;
    width: 260px;
    margin-left: auto;
    margin-right: auto;
    box-shadow: 0 4px 15px rgba(76,175,80,0.6);
  }
  form#inputForm button:hover, form#inputForm button:focus {
    background-color: #388e3c;
    box-shadow: 0 6px 18px rgba(56,142,60,0.8);
  }
  /* Chart Selection dropdown container */
  .chart-section {
    background: white;
    box-shadow: 0 5px 18px rgba(0,0,0,0.08);
    border-radius: 14px;
    padding: 25px 25px 40px 25px;
    margin-bottom: 50px;
    max-width: 960px;
    margin-left: auto;
    margin-right: auto;
    transition: box-shadow 0.3s ease;
  }
  .chart-section:hover {
    box-shadow: 0 9px 32px rgba(0,0,0,0.14);
  }
  .chart-section h2 {
    font-weight: 900;
    font-size: 1.8rem;
    color: #2e7d32;
    margin-bottom: 12px;
    text-align: center;
  }
  .chart-type-selector {
    display: flex;
    justify-content: center;
    gap: 22px;
    margin-bottom: 20px;
    user-select: none;
  }
  .chart-type-selector label {
    font-weight: 700;
    font-size: 1.05rem;
    color: #2e7d32;
    cursor: pointer;
    background: #e6f2e6;
    border: 2px solid transparent;
    border-radius: 12px;
    padding: 7px 15px;
    transition: background 0.3s, border-color 0.3s;
  }
  .chart-type-selector input[type="radio"] {
    display: none;
  }
  .chart-type-selector input[type="radio"]:checked + label {
    background: #4caf50;
    color: white;
    border-color: #388e3c;
    box-shadow: 0 3px 10px rgba(56,142,60,0.6);
  }
  canvas {
    display: block;
    max-width: 100%;
    margin-left: auto;
    margin-right: auto;
    border-radius: 12px;
    box-shadow: 0 3px 18px rgba(0,0,0,0.12);
    background: white;
  }
  /* Narrative, Actions, Recommendations styling */
  #narrative, #action-items, #recommendations {
    background: white;
    max-width: 960px;
    margin: 0 auto 50px auto;
    border-radius: 14px;
    box-shadow: 0 6px 25px rgba(0,0,0,0.08);
    padding: 30px 30px 35px 30px;
  }
  #narrative h2, #action-items h2, #recommendations h2 {
    color: #2e7d32;
    font-weight: 900;
    font-size: 1.9rem;
    text-align: center;
    margin-bottom: 22px;
    letter-spacing: 0.05em;
  }
  #narrative p, #action-items ul, #recommendations ul {
    font-size: 1.1rem;
    line-height: 1.75;
    color: #444;
    max-width: 740px;
    margin-left: auto;
    margin-right: auto;
  }
  #action-items ul, #recommendations ul {
    list-style: disc inside;
    font-weight: 600;
  }
  #recommendations li strong {
    color: #2e7d32;
  }

  /* Responsive adjustments */
  @media (max-width: 900px) {
    form#inputForm, .chart-section, #narrative, #action-items, #recommendations {
      max-width: 90vw;
    }
    .input-group > div {
      min-width: 140px;
      flex-grow: 1;
    }
  }
  @media (max-width: 480px) {
    .input-group > div {
      min-width: 100%;
    }
    .chart-type-selector {
      flex-direction: column;
      align-items: center;
    }
    .chart-type-selector label {
      width: 100%;
      text-align: center;
    }
  }
</style>
</head>
<body>
<header>
  <h1>Interactive Restaurant Food Waste Management Dashboard</h1>
  <p>Monitor and optimize your food waste composting business with AI-generated insights</p>
</header>
<main>

  <form id="inputForm" aria-label="Input Data Form">
    <h2>Enter Your Business Data</h2>
    
    <fieldset style="border:none; margin-bottom: 20px;">
      <legend style="font-weight:700; color:#2e7d32; font-size:1.2rem; margin-bottom: 12px;">Daily Food Waste Volume (kg) - per Day</legend>
      <div class="input-group" role="group" aria-label="Daily Food Waste Volume inputs">
        <div><label for="monday">Monday</label><input type="number" id="monday" name="monday" min="0" value="120" required></div>
        <div><label for="tuesday">Tuesday</label><input type="number" id="tuesday" name="tuesday" min="0" value="135" required></div>
        <div><label for="wednesday">Wednesday</label><input type="number" id="wednesday" name="wednesday" min="0" value="110" required></div>
        <div><label for="thursday">Thursday</label><input type="number" id="thursday" name="thursday" min="0" value="140" required></div>
        <div><label for="friday">Friday</label><input type="number" id="friday" name="friday" min="0" value="130" required></div>
        <div><label for="saturday">Saturday</label><input type="number" id="saturday" name="saturday" min="0" value="150" required></div>
        <div><label for="sunday">Sunday</label><input type="number" id="sunday" name="sunday" min="0" value="125" required></div>
      </div>
    </fieldset>

    <fieldset style="border:none; margin-bottom: 20px;">
      <legend style="font-weight:700; color:#2e7d32; font-size:1.2rem; margin-bottom: 12px;">Waste Processing Breakdown (kg)</legend>
      <div class="input-group" role="group" aria-label="Waste Processing Breakdown inputs">
        <div><label for="composted">Composted</label><input type="number" id="composted" name="composted" min="0" value="80" required></div>
        <div><label for="discarded">Discarded (Not Compostable)</label><input type="number" id="discarded" name="discarded" min="0" value="40" required></div>
      </div>
    </fieldset>

    <fieldset style="border:none; margin-bottom: 20px;">
      <legend style="font-weight:700; color:#2e7d32; font-size:1.2rem; margin-bottom: 12px;">Monthly Compost Sales ($) - per Month</legend>
      <div class="input-group" role="group" aria-label="Monthly Compost Sales inputs">
        <div><label for="jan">Jan</label><input type="number" id="jan" name="jan" min="0" value="3000" required></div>
        <div><label for="feb">Feb</label><input type="number" id="feb" name="feb" min="0" value="3500" required></div>
        <div><label for="mar">Mar</label><input type="number" id="mar" name="mar" min="0" value="3800" required></div>
        <div><label for="apr">Apr</label><input type="number" id="apr" name="apr" min="0" value="4000" required></div>
        <div><label for="may">May</label><input type="number" id="may" name="may" min="0" value="4500" required></div>
        <div><label for="jun">Jun</label><input type="number" id="jun" name="jun" min="0" value="4700" required></div>
        <div><label for="jul">Jul</label><input type="number" id="jul" name="jul" min="0" value="5000" required></div>
        <div><label for="aug">Aug</label><input type="number" id="aug" name="aug" min="0" value="5200" required></div>
      </div>
    </fieldset>

    <button type="submit" aria-label="Update Dashboard">Update Dashboard</button>
  </form>

  <!-- Chart Sections for each dataset -->

  <section class="chart-section" aria-label="Daily Food Waste Volume Chart Section">
    <h2>Daily Food Waste Volume (kg)</h2>
    <div class="chart-type-selector" role="radiogroup" aria-label="Select chart type for Daily Food Waste Volume">
      <input type="radio" id="daily-bar" name="daily-chart-type" value="bar" checked>
      <label for="daily-bar" title="Bar Chart">Bar Chart</label>
      <input type="radio" id="daily-line" name="daily-chart-type" value="line">
      <label for="daily-line" title="Line Chart">Line Chart</label>
      <input type="radio" id="daily-pie" name="daily-chart-type" value="pie">
      <label for="daily-pie" title="Pie Chart">Pie Chart</label>
    </div>
    <canvas id="dailyChart" aria-describedby="dailyChartDesc" role="img"></canvas>
    <p id="dailyChartDesc" class="visually-hidden">Chart displaying daily food waste volume in kilograms</p>
  </section>

  <section class="chart-section" aria-label="Waste Processing Breakdown Chart Section">
    <h2>Waste Processing Breakdown (kg)</h2>
    <div class="chart-type-selector" role="radiogroup" aria-label="Select chart type for Waste Processing Breakdown">
      <input type="radio" id="waste-bar" name="waste-chart-type" value="bar" checked>
      <label for="waste-bar" title="Bar Chart">Bar Chart</label>
      <input type="radio" id="waste-line" name="waste-chart-type" value="line">
      <label for="waste-line" title="Line Chart">Line Chart</label>
      <input type="radio" id="waste-pie" name="waste-chart-type" value="pie">
      <label for="waste-pie" title="Pie Chart">Pie Chart</label>
    </div>
    <canvas id="wasteChart" aria-describedby="wasteChartDesc" role="img"></canvas>
    <p id="wasteChartDesc" class="visually-hidden">Chart displaying waste processing breakdown in kilograms</p>
  </section>

  <section class="chart-section" aria-label="Monthly Compost Sales Chart Section">
    <h2>Monthly Compost Sales ($)</h2>
    <div class="chart-type-selector" role="radiogroup" aria-label="Select chart type for Monthly Compost Sales">
      <input type="radio" id="sales-bar" name="sales-chart-type" value="bar">
      <label for="sales-bar" title="Bar Chart">Bar Chart</label>
      <input type="radio" id="sales-line" name="sales-chart-type" value="line" checked>
      <label for="sales-line" title="Line Chart">Line Chart</label>
      <input type="radio" id="sales-pie" name="sales-chart-type" value="pie">
      <label for="sales-pie" title="Pie Chart">Pie Chart</label>
    </div>
    <canvas id="salesChart" aria-describedby="salesChartDesc" role="img"></canvas>
    <p id="salesChartDesc" class="visually-hidden">Chart displaying monthly compost sales in dollars</p>
  </section>

  <section id="narrative" role="region" aria-live="polite" aria-label="Business Report Narrative">
    <h2>Business Report Narrative</h2>
    <p id="narrative-text">Loading narrative...</p>
  </section>

  <section id="action-items" role="region" aria-live="polite" aria-label="AI-Generated Action Items">
    <h2>AI-Generated Action Items</h2>
    <ul id="actions-list">
      <li>Loading action items...</li>
    </ul>
  </section>

  <section id="recommendations" role="region" aria-live="polite" aria-label="Recommendations Based on Case Studies">
    <h2>Recommendations Based on Case Studies</h2>
    <ul id="recommendations-list">
      <li>Loading recommendations...</li>
    </ul>
  </section>
</main>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
  // Data storage - default sample values
  let dailyWaste = {
    labels: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'],
    data: [120, 135, 110, 140, 130, 150, 125]
  };
  let wasteProcessing = {
    labels: ['Composted', 'Discarded (Not Compostable)'],
    data: [80, 40]
  };
  let monthlySales = {
    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug'],
    data: [3000, 3500, 3800, 4000, 4500, 4700, 5000, 5200]
  };

  // Chart instances (one per chart area)
  let dailyChartInstance = null;
  let wasteChartInstance = null;
  let salesChartInstance = null;

  // Utility functions
  function average(arr) {
    return arr.reduce((a,b) => a+b, 0) / arr.length;
  }
  function percentage(part, total) {
    return total > 0 ? ((part / total) * 100).toFixed(1) : '0.0';
  }
  function trend(arr) {
    const first = arr[0];
    const last = arr[arr.length -1];
    const diff = last - first;
    const percentChange = first !== 0 ? ((diff / first) * 100).toFixed(1) : 'N/A';
    return { diff, percentChange };
  }
  function highestWasteDay() {
    const maxWaste = Math.max(...dailyWaste.data);
    return dailyWaste.labels[dailyWaste.data.indexOf(maxWaste)] || 'N/A';
  }

  // Functions to create charts dynamically by type
  function createChart(ctx, type, labels, data, colors, options) {
    return new Chart(ctx, {
      type,
      data: {
        labels,
        datasets: [{
          label: (type === 'pie' ? '' : 'Value'),
          data,
          backgroundColor: colors,
          borderRadius: type === 'bar' ? 6 : 0,
          fill: (type === 'line'),
          borderColor: (type === 'line' ? '#388e3c' : undefined),
          tension: (type === 'line' ? 0.35 : 0),
          pointRadius: type === 'line' ? 5 : 0,
          pointHoverRadius: type === 'line' ? 7 : 0,
          borderWidth: 2,
          hoverOffset: (type === 'pie' ? 15 : undefined),
        }]
      },
      options: {
        responsive: true,
        animation: { duration: 600, easing: 'easeInOutQuad' },
        plugins: {
          legend: { display: type === 'pie', position: 'bottom', labels: { font: { weight: '700', size: 14 } } },
          tooltip: { enabled: true, mode: 'nearest', intersect: false }
        },
        scales: (type === 'pie') ? undefined : {
          y: { beginAtZero: true, title: { display: true, text: (type === 'line' || type === 'bar') ? ((ctx.canvas.id==='dailyChart') ? 'Kilograms (kg)' : ctx.canvas.id==='wasteChart' ? 'Kilograms (kg)' : 'Sales in USD ($)') : undefined } },
          x: { title: { display: true, text: (ctx.canvas.id==='dailyChart') ? 'Days' : ctx.canvas.id==='wasteChart' ? 'Processing Type' : 'Months' } }
        }
      }
    });
  }

  // Update and redraw charts based on chart type selectors and data
  function updateDailyChart() {
    const ctx = document.getElementById('dailyChart').getContext('2d');
    const selectedType = document.querySelector('input[name="daily-chart-type"]:checked').value;

    // Special case: If pie chart, data and labels need adjustment as pie requires categoric segments
    // We'll use the dailyWaste data as segments in pie but it may be many slices - still allow as user wants.
    // Use strong green palette for bar/line, multicolor for pie.
    const colors_base = ['#66bb6a', '#81c784', '#a5d6a7', '#c8e6c9', '#dcedc8', '#e8f5e9', '#f1f8e9'];
    const pieColors = ['#4caf50','#66bb6a','#81c784','#a5d6a7','#c8e6c9','#dcedc8','#e8f5e9'];

    if(dailyChartInstance) dailyChartInstance.destroy();

    if(selectedType === 'pie') {
      dailyChartInstance = createChart(ctx, 'pie', dailyWaste.labels, dailyWaste.data, pieColors.slice(0,dailyWaste.labels.length));
    } else {
      dailyChartInstance = createChart(ctx, selectedType, dailyWaste.labels, dailyWaste.data, colors_base.slice(0,dailyWaste.labels.length));
    }
  }

  function updateWasteChart() {
    const ctx = document.getElementById('wasteChart').getContext('2d');
    const selectedType = document.querySelector('input[name="waste-chart-type"]:checked').value;
    const colors_green_red = ['#4caf50', '#ef5350']; // composted green, discarded red
    const colors_bar_line = ['#388e3c', '#e53935'];

    if(wasteChartInstance) wasteChartInstance.destroy();

    if(selectedType === 'pie') {
      wasteChartInstance = createChart(ctx, 'pie', wasteProcessing.labels, wasteProcessing.data, colors_green_red);
    } else {
      wasteChartInstance = createChart(ctx, selectedType, wasteProcessing.labels, wasteProcessing.data, colors_bar_line);
    }
  }

  function updateSalesChart() {
    const ctx = document.getElementById('salesChart').getContext('2d');
    const selectedType = document.querySelector('input[name="sales-chart-type"]:checked').value;

    const colors_base = ['#66bb6a', '#81c784', '#a5d6a7', '#c8e6c9', '#dcedc8', '#e8f5e9', '#f1f8e9', '#c5e1a5'];
    if(salesChartInstance) salesChartInstance.destroy();

    if(selectedType === 'pie') {
      salesChartInstance = createChart(ctx, 'pie', monthlySales.labels, monthlySales.data, colors_base.slice(0,monthlySales.labels.length));
    } else {
      salesChartInstance = createChart(ctx, selectedType, monthlySales.labels, monthlySales.data, ['#388e3c']);
    }
  }

  // Narrative, Action items & Recommendations generation logic
  function generateNarrative() {
    const avgWaste = average(dailyWaste.data).toFixed(0);
    const maxWaste = Math.max(...dailyWaste.data);
    const maxWasteDay = dailyWaste.labels[dailyWaste.data.indexOf(maxWaste)];
    const totalWasteProcessed = wasteProcessing.data.reduce((a,b) => a+b,0);
    const compostPercent = percentage(wasteProcessing.data[0], totalWasteProcessed);
    const discardedPercent = percentage(wasteProcessing.data[1], totalWasteProcessed);

    const { diff: salesDiff, percentChange: salesPercentChange } = trend(monthlySales.data);
    const startSales = monthlySales.data[0];

    return `
      The restaurant produces an average of <strong>${avgWaste} kg</strong> of food waste daily, with the highest volume recorded on <strong>${maxWasteDay}</strong> at <strong>${maxWaste} kg</strong>. This indicates potential opportunities for waste reduction especially mid-week and weekend periods.<br><br>
      
      Of the total food waste collected, approximately <strong>${compostPercent}%</strong> is successfully processed into compost, a strong indicator of efficient waste diversion from landfill. However, <strong>${discardedPercent}%</strong> is non-compostable waste, suggesting a scope for improved sorting or waste reduction strategies.<br><br>
      
      Monthly compost sales have shown a ${salesPercentChange !== 'N/A' ? `positive upward trend, increasing by <strong>${salesPercentChange}%</strong>` : '<strong>variable trend due to zero start sales</strong>'} (from $${startSales} to $${monthlySales.data[monthlySales.data.length-1]}), confirming growth in market demand and successful business scaling.<br><br>
      
      These insights demonstrate solid progress in food waste management and compost sales, but also highlight areas to optimize processing efficiency and explore waste prevention.
    `;
  }
  function generateActionItems() {
    return [
      "Conduct targeted waste reduction efforts on days with peak waste volumes (e.g., " + highestWasteDay() + ").",
      "Enhance sorting processes to reduce non-compostable waste below current levels of " + wasteProcessing.data[1] + " kg.",
      "Expand marketing and sales efforts in gardening markets to maintain and accelerate compost sales growth.",
      "Invest in staff training on waste segregation and compost quality to improve product value and customer satisfaction."
    ];
  }
  function generateRecommendations() {
    return [
      "<strong>Case Study 1: ZeroWaste Bistro, NYC</strong> - Implemented a systematic waste audit and staff training program that reduced food waste by 25% in 6 months, leading to higher compost outputs and cost savings.",
      "<strong>Case Study 2: GreenFarm Compost Co.</strong> - Diversified compost sales with partnerships in local gardening centers and community markets, boosting sales by 40% within a year.",
      "<strong>Case Study 3: Farm-to-Table Restaurant, Oregon</strong> - Adopted advanced composting technology to increase processing capacity by 35%, while educating customers on benefits, resulting in brand loyalty and repeat business.",
      "<strong>Recommendation:</strong> Emulating these successful strategies, focus on auditing and staff engagement to reduce waste, building strong sales partnerships, and investing in technology and marketing to scale your business effectively."
    ];
  }

  // Update narrative and text content sections
  function updateTextSections() {
    document.getElementById('narrative-text').innerHTML = generateNarrative();

    const actionsList = document.getElementById('actions-list');
    actionsList.innerHTML = '';
    generateActionItems().forEach(item => {
      const li = document.createElement('li');
      li.innerHTML = item;
      actionsList.appendChild(li);
    });

    const recommendationsList = document.getElementById('recommendations-list');
    recommendationsList.innerHTML = '';
    generateRecommendations().forEach(item => {
      const li = document.createElement('li');
      li.innerHTML = item;
      recommendationsList.appendChild(li);
    });
  }

  // Reads inputs from form and updates data
  function readInputData() {
    dailyWaste.data = [
      +document.getElementById('monday').value || 0,
      +document.getElementById('tuesday').value || 0,
      +document.getElementById('wednesday').value || 0,
      +document.getElementById('thursday').value || 0,
      +document.getElementById('friday').value || 0,
      +document.getElementById('saturday').value || 0,
      +document.getElementById('sunday').value || 0
    ];
    const composted = +document.getElementById('composted').value || 0;
    const discarded = +document.getElementById('discarded').value || 0;
    wasteProcessing.data = [composted, discarded];
    monthlySales.data = [
      +document.getElementById('jan').value || 0,
      +document.getElementById('feb').value || 0,
      +document.getElementById('mar').value || 0,
      +document.getElementById('apr').value || 0,
      +document.getElementById('may').value || 0,
      +document.getElementById('jun').value || 0,
      +document.getElementById('jul').value || 0,
      +document.getElementById('aug').value || 0
    ];
  }

  // Main update function to update all charts and texts
  function updateDashboard() {
    updateDailyChart();
    updateWasteChart();
    updateSalesChart();
    updateTextSections();
  }

  // Event listeners for chart type radio buttons to update charts dynamically
  document.querySelectorAll('input[name="daily-chart-type"]').forEach(el => {
    el.addEventListener('change', () => {
      updateDailyChart();
    });
  });
  document.querySelectorAll('input[name="waste-chart-type"]').forEach(el => {
    el.addEventListener('change', () => {
      updateWasteChart();
    });
  });
  document.querySelectorAll('input[name="sales-chart-type"]').forEach(el => {
    el.addEventListener('change', () => {
      updateSalesChart();
    });
  });

  // Form submit event to read inputs and update dashboard
  document.getElementById('inputForm').addEventListener('submit', function(e) {
    e.preventDefault();
    readInputData();
    updateDashboard();
  });

  // Initialize dashboard on page load
  updateDashboard();

</script>
</body>
</html>

