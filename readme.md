# Interactive Data Visualization

This repository contains a web application that demonstrates interactive data visualization using [Chart.js](https://www.chartjs.org/) and [Anime.js](https://animejs.com/). It creates an animated bar chart displaying monthly sales data.

## Prerequisites

Before you start, make sure you have the following:

- A modern web browser
- Internet access to load Chart.js and Anime.js libraries from CDNs

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Interactive Data Visualization</title>
    <link rel="stylesheet" href="./style.css">
</head>
<body>
    <div class="chart-container">
        <canvas id="myChart"></canvas>
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.7.0/chart.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/animejs/3.2.1/anime.min.js"></script>
    <script src="./script.js"></script>
</body>
</html>
```

## JavaScript (script.js) Explanation

```javascript
const data = {
    labels: ['January', 'February', 'March', 'April', 'May'],
    datasets: [{
        label: 'Monthly Sales',
        backgroundColor: 'rgba(75, 192, 192, 0.2)',
        borderColor: 'rgba(75, 192, 192, 1)',
        borderWidth: 1,
        data: [65, 59, 80, 81, 56],
    }],
};
```

- This code defines the data for the chart, including labels (months) and sales data for each month.

```javascript
const config = {
    type: 'bar',
    data: data,
    options: {
        responsive: true,
        plugins: {
            title: {
                display: true,
                text: 'Monthly Sales Data',
            },
        },
    },
};
```

- `config` is an object that configures the chart type (bar chart), data (from `data`), and various chart options.
- It includes responsiveness and a title for the chart.

```javascript
const ctx = document.getElementById('myChart').getContext('2d');
const myChart = new Chart(ctx, config);
```

- This code initializes the Chart.js chart using the canvas context (`ctx`) and the configuration object (`config`).

```javascript
myChart.options.plugins.tooltip = {
    callbacks: {
        label: function (context) {
            return `Sales: ${context.parsed.y}`;
        },
    },
};
```

- It customizes the tooltip to display the sales value when hovering over a bar.

```javascript
const chartAnimation = anime({
    targets: myChart.data.datasets[0].data,
    easing: 'linear',
    delay: anime.stagger(200),
    duration: 1000,
    loop: true,
    direction: 'alternate',
    update: function (anim) {
        myChart.update();
    },
});
```

- This code uses Anime.js to animate the chart.
- It targets the data of the chart's dataset, specifying animation properties like easing, delay, duration, loop, and direction.
- The `update` function is called to update the chart during the animation.

## Usage

1. Clone or download this repository to your local machine.
2. Open the `index.html` file in a web browser to view the interactive bar chart displaying monthly sales data.

