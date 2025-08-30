---
layout: default
title: Cosmic Graph Visualization
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cosmic Graph Visualization</title>
    <link rel="stylesheet" href="{{ '/assets/css/style.css' | relative_url }}">
</head>
<body>
    <header>
        <h1>Cosmic Graph Visualization</h1>
        <p class="subtitle">A Mathematical Representation of Cosmic Patterns</p>
    </header>
    
    <div class="container">
        <div class="graph-container">
            <canvas id="cosmicGraph"></canvas>
        </div>
        
        <div class="explanation">
            <h2>About the Cosmic Graph</h2>
            <p>The cosmic graph is a complex mathematical visualization that combines several elements to represent cosmic patterns and mathematical relationships.</p>
            
            <h3>1. Polar Coordinate System</h3>
            <p>The graph is drawn on a polar coordinate system with:</p>
            <ul>
                <li><strong>Radial lines</strong> extending from the center at 15-degree intervals</li>
                <li><strong>Concentric circles</strong> at regular intervals from the center</li>
            </ul>
            
            <h3>2. Mathematical Function</h3>
            <p>The main spiral pattern is generated using a combination of trigonometric functions:</p>
            <p class="code-sample">y = sin(x) * x * cos(x)</p>
            <p>This creates an oscillating pattern that increases in amplitude as it moves outward.</p>
            
            <h3>3. Mapping to Polar Coordinates</h3>
            <p>The function is mapped to polar coordinates using:</p>
            <ul>
                <li><strong>Angle (θ)</strong>: Determines the direction from the center</li>
                <li><strong>Radius</strong>: Determined by the output of the mathematical function</li>
            </ul>
            
            <h3>4. Technical Implementation</h3>
            <p>The graph is drawn on an HTML5 Canvas using these key steps:</p>
            
            <div class="code-sample">// 1. Draw radial lines
for (let angle = 0; angle < 360; angle += 15) {
    const rad = angle * Math.PI / 180;
    ctx.beginPath();
    ctx.moveTo(centerX, centerY);
    ctx.lineTo(centerX + Math.cos(rad) * maxRadius, centerY + Math.sin(rad) * maxRadius);
    ctx.stroke();
}

// 2. Draw concentric circles
for (let r = 50; r <= maxRadius; r += 50) {
    ctx.beginPath();
    ctx.arc(centerX, centerY, r, 0, Math.PI * 2);
    ctx.stroke();
}

// 3. Calculate and draw the spiral graph
const points = [];
for (let i = 0; i <= 1000; i++) {
    const theta = (i / 1000) * Math.PI * 2;
    const x = -180 + (360 * theta / (Math.PI * 2));
    const y = Math.sin(x) * x * cos(x);
    const radius = minRadius + ((maxRadius - minRadius) * (y + 180) / 360);
    const graphX = centerX + Math.cos(theta - Math.PI/2) * radius;
    const graphY = centerY + Math.sin(theta - Math.PI/2) * radius;
    
    points.push({x: graphX, y: graphY});
}

// 4. Draw the path
ctx.beginPath();
points.forEach(point => ctx.lineTo(point.x, point.y));
ctx.stroke();</div>
            
            <h3>Interpretation</h3>
            <p>The cosmic graph represents the complex, interconnected nature of the universe, with:</p>
            <ul>
                <li>The center representing a singularity or origin point</li>
                <li>The radial lines representing fundamental forces or dimensions</li>
                <li>The spiral pattern representing the evolution of cosmic structures over time</li>
                <li>The oscillating nature suggesting cycles of expansion and contraction</li>
            </ul>
            
            <center>
                <a href="https://github.com/your-username/your-repo" class="github-btn">View on GitHub</a>
            </center>
        </div>
    </div>

    <footer>
        <p>Created for GitHub Pages | &copy; 2023</p>
    </footer>

    <script>
        function drawCosmicGraph() {
            const canvas = document.getElementById('cosmicGraph');
            const container = document.querySelector('.graph-container');
            
            // Set canvas size to match container
            canvas.width = container.clientWidth;
            canvas.height = container.clientHeight;
            
            const ctx = canvas.getContext('2d');
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            
            // Scale the radius based on container size
            const maxRadius = Math.min(centerX, centerY) * 0.8;
            const minRadius = maxRadius * 0.2;
            
            // Clear the canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // Set styles for the coordinate system - thinner lines
            ctx.strokeStyle = '#333';
            ctx.lineWidth = 0.5;  // Thinner lines
            ctx.fillStyle = '#000';
            
            // Draw radial lines
            for (let angle = 0; angle < 360; angle += 15) {
                const rad = angle * Math.PI / 180;
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(centerX + Math.cos(rad) * maxRadius * 1.1, centerY + Math.sin(rad) * maxRadius * 1.1);
                ctx.stroke();
            }
            
            // Draw concentric circles
            const circleStep = maxRadius / 5;
            for (let r = circleStep; r <= maxRadius; r += circleStep) {
                ctx.beginPath();
                ctx.arc(centerX, centerY, r, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Create and draw the complex spiral graph with thinner lines
            const points = [];
            ctx.strokeStyle = '#1a237e';  // Dark blue color
            ctx.lineWidth = 1.5;  // Thinner main line
            ctx.beginPath();
            
            for (let i = 0; i <= 1000; i++) {
                const theta = (i / 1000) * Math.PI * 2;
                const x = -180 + (360 * theta / (Math.PI * 2));
                const y = Math.sin(x) * x * Math.cos(x);
                const radius = minRadius + ((maxRadius - minRadius) * (y + 180) / 360);
                const graphX = centerX + Math.cos(theta - Math.PI/2) * radius;
                const graphY = centerY + Math.sin(theta - Math.PI/2) * radius;
                
                if (i === 0) ctx.moveTo(graphX, graphY);
                else ctx.lineTo(graphX, graphY);
                
                points.push({x: graphX, y: graphY});
            }
            
            ctx.stroke();
            
            // Add a slightly thicker line for emphasis (but still thinner than before)
            ctx.strokeStyle = '#3949ab';
            ctx.lineWidth = 2;  // Thinner emphasis line
            ctx.beginPath();
            points.forEach(point => ctx.lineTo(point.x, point.y));
            ctx.stroke();
            
            // Add smaller dots along the graph line
            points.forEach((point, i) => {
                if (i % 20 === 0) {
                    ctx.fillStyle = '#3949ab';
                    ctx.beginPath();
                    ctx.arc(point.x, point.y, 2, 0, Math.PI * 2);  // Smaller dots
                    ctx.fill();
                }
            });
        }
        
        // Draw the graph when the page loads
        window.onload = drawCosmicGraph;
        
        // Redraw when window is resized
        window.addEventListener('resize', drawCosmicGraph);
    </script>
</body>
</html>
