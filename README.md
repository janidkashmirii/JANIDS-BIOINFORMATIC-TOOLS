<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Janids Bioinformatic Tools - Heatmap Generator</title>
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f9;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        textarea {
            width: 100%;
            height: 150px;
            margin: 10px 0;
            padding: 10px;
            font-size: 14px;
        }
        button {
            background-color: #007bff;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
        #heatmap {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Janids Bioinformatic Tools - Heatmap Generator</h1>
        <p>Enter your data in CSV format (e.g., rows separated by newlines, columns by commas):</p>
        <textarea id="dataInput" placeholder="Enter data (e.g., 1,2,3\n4,5,6\n7,8,9)"></textarea>
        <button onclick="generateHeatmap()">Generate Heatmap</button>
        <div id="heatmap"></div>
    </div>

    <script>
        function generateHeatmap() {
            const input = document.getElementById('dataInput').value.trim();
            if (!input) {
                alert('Please enter data in CSV format.');
                return;
            }

            // Parse CSV input
            const rows = input.split('\n').map(row => row.split(',').map(Number));
            const zData = rows;

            // Validate data
            if (zData.length === 0 || zData.some(row => row.length !== zData[0].length)) {
                alert('Invalid data format. Ensure all rows have the same number of columns.');
                return;
            }

            // Create heatmap
            const data = [{
                z: zData,
                type: 'heatmap',
                colorscale: 'Viridis',
                showscale: true
            }];

            const layout = {
                title: 'Heatmap',
                xaxis: { title: 'Columns' },
                yaxis: { title: 'Rows' },
                margin: { t: 50, r: 50, b: 50, l: 50 }
            };

            Plotly.newPlot('heatmap', data, layout);
        }
    </script>
</body>
</html>
