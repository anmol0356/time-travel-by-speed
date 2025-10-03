<CREATED BY ANMOL SINGH>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Time Dilation Explorer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 40px;
        }
        
        h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 0 0 20px rgba(255,255,255,0.5);
        }
        
        .subtitle {
            font-size: 1.3em;
            opacity: 0.9;
        }
        
        .tabs {
            display: flex;
            gap: 15px;
            margin-bottom: 30px;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .tab-btn {
            padding: 15px 30px;
            background: rgba(255,255,255,0.1);
            border: 2px solid rgba(255,255,255,0.3);
            border-radius: 10px;
            color: white;
            cursor: pointer;
            font-size: 1.1em;
            transition: all 0.3s;
        }
        
        .tab-btn:hover {
            background: rgba(255,255,255,0.2);
            transform: translateY(-3px);
        }
        
        .tab-btn.active {
            background: rgba(255,255,255,0.3);
            border-color: white;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .section {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            border: 1px solid rgba(255,255,255,0.2);
        }
        
        h2 {
            color: #ffd700;
            margin-bottom: 20px;
            font-size: 2em;
        }
        
        h3 {
            color: #ffeb3b;
            margin: 20px 0 15px 0;
            font-size: 1.5em;
        }
        
        p {
            line-height: 1.8;
            margin-bottom: 15px;
            font-size: 1.1em;
        }
        
        .canvas-container {
            background: rgba(0,0,0,0.3);
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            border: 2px solid rgba(255,255,255,0.2);
        }
        
        canvas {
            display: block;
            margin: 0 auto;
            background: rgba(0,0,0,0.5);
            border-radius: 8px;
        }
        
        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }
        
        .control-group {
            background: rgba(255,255,255,0.1);
            padding: 20px;
            border-radius: 10px;
        }
        
        .control-group label {
            display: block;
            font-weight: bold;
            margin-bottom: 10px;
            color: #ffd700;
        }
        
        input[type="range"] {
            width: 100%;
            margin: 10px 0;
        }
        
        input[type="number"] {
            width: 100%;
            padding: 10px;
            border-radius: 5px;
            border: none;
            font-size: 1em;
        }
        
        .value-display {
            text-align: center;
            font-size: 1.3em;
            color: #4fc3f7;
            font-weight: bold;
            margin: 10px 0;
        }
        
        .formula-box {
            background: rgba(0,0,0,0.3);
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            border-left: 5px solid #ffd700;
        }
        
        .formula {
            font-family: 'Courier New', monospace;
            font-size: 1.3em;
            text-align: center;
            margin: 15px 0;
            color: #4fc3f7;
        }
        
        .result-box {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        
        .result-value {
            font-size: 2.5em;
            font-weight: bold;
            margin: 15px 0;
            color: #ffd700;
        }
        
        .info-card {
            background: rgba(255,255,255,0.05);
            padding: 20px;
            border-radius: 10px;
            margin: 15px 0;
            border-left: 4px solid #4fc3f7;
        }
        
        .warning {
            background: rgba(255,152,0,0.2);
            border-left-color: #ff9800;
            border: 2px solid #ff9800;
        }
        
        button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 8px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s;
            margin: 10px 5px;
        }
        
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 20px rgba(102,126,234,0.5);
        }
        
        .calculator {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        
        @media (max-width: 768px) {
            h1 { font-size: 2em; }
            .calculator { grid-template-columns: 1fr; }
        }
        
        .equation {
            background: rgba(0,0,0,0.4);
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
            text-align: center;
            font-size: 1.2em;
        }
        
        .spaceship {
            position: absolute;
            width: 40px;
            height: 20px;
            background: linear-gradient(90deg, #ff6b6b 0%, #ee5a6f 100%);
            clip-path: polygon(0% 50%, 20% 0%, 80% 0%, 100% 50%, 80% 100%, 20% 100%);
            box-shadow: 0 0 20px #ff6b6b;
        }
        
        .clock {
            font-size: 2em;
            font-weight: bold;
            text-align: center;
            margin: 10px 0;
            font-family: 'Courier New', monospace;
        }

        .watermark {
            position: fixed;
            bottom: 10px;
            right: 10px;
            opacity: 0.5;
            font-size: 0.8em;
            color: white;
            z-index: 1000;
            text-align: right;
        }

        .watermark a {
            color: white;
            text-decoration: none;
            transition: opacity 0.3s;
        }

        .watermark a:hover {
            opacity: 1;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Time Dilation & Relativistic Physics</h1>
            <p class="subtitle">Explore Einstein's Special Relativity through Interactive Animations</p>
        </header>
        
        <div class="tabs">
            <button class="tab-btn active" onclick="showTab('animation')">Visual Animation</button>
            <button class="tab-btn" onclick="showTab('theory')">The Science</button>
            <button class="tab-btn" onclick="showTab('calculator')">Calculators</button>
            <button class="tab-btn" onclick="showTab('examples')">Real Examples</button>
        </div>
        
        <!-- ANIMATION TAB -->
        <div id="animation" class="tab-content active">
            <div class="section">
                <h2>Time Dilation Visualizer</h2>
                <p>Watch how time slows down for a moving spaceship compared to a stationary observer on Earth. The faster the spaceship moves (closer to light speed), the more dramatic the effect!</p>
                
                <div class="canvas-container">
                    <canvas id="timeCanvas" width="800" height="400"></canvas>
                    <div style="display: flex; justify-content: space-around; margin-top: 20px;">
                        <div>
                            <div style="color: #4fc3f7; font-weight: bold;">Earth Clock</div>
                            <div class="clock" id="earthClock">00:00</div>
                        </div>
                        <div>
                            <div style="color: #ff6b6b; font-weight: bold;">Spaceship Clock</div>
                            <div class="clock" id="shipClock">00:00</div>
                        </div>
                    </div>
                </div>
                
                <div class="controls">
                    <div class="control-group">
                        <label>Speed (as fraction of light speed c):</label>
                        <input type="range" id="speedSlider" min="0" max="99" value="0" step="1">
                        <div class="value-display">
                            <span id="speedPercent">0</span>% of light speed<br>
                            <small><span id="speedKmh">0</span> km/h</small>
                        </div>
                    </div>
                    
                    <div class="control-group">
                        <label>Time Dilation Factor (γ):</label>
                        <div class="value-display" id="gamma" style="font-size: 2em;">1.000</div>
                        <p style="font-size: 0.9em; margin-top: 10px;">For every 1 second on the spaceship, <span id="earthTime">1.00</span> seconds pass on Earth</p>
                    </div>
                </div>
                
                <div style="text-align: center; margin: 20px 0;">
                    <button onclick="startAnimation()">Start/Resume</button>
                    <button onclick="pauseAnimation()">Pause</button>
                    <button onclick="resetAnimation()">Reset</button>
                </div>
                
                <div class="info-card warning">
                    <h3>Key Observation:</h3>
                    <p>Notice how at low speeds (below 50% light speed), time dilation is minimal. But as you approach 90-99% light speed, time on the spaceship slows dramatically compared to Earth. At 99% light speed, the spaceship ages only about 1/7th as fast as Earth!</p>
                </div>
            </div>
        </div>
        
        <!-- THEORY TAB -->
        <div id="theory" class="tab-content">
            <div class="section">
                <h2>Understanding Time Dilation</h2>
                
                <h3>What is Time Dilation?</h3>
                <p>Time dilation is a real physical phenomenon predicted by Einstein's Special Theory of Relativity (1905). It states that time passes at different rates for objects moving at different speeds. The faster you move relative to someone else, the slower time passes for you from their perspective.</p>
                
                <div class="info-card">
                    <h3>The Twin Paradox Example</h3>
                    <p>Imagine twins: one stays on Earth, the other travels in a spaceship at near-light speed. When the traveling twin returns, they will have aged less than the Earth-bound twin. This isn't science fiction—it's proven physics!</p>
                </div>
                
                <h3>How Fast is the Speed of Light?</h3>
                <div class="formula-box">
                    <div class="formula">c = 299,792,458 meters/second</div>
                    <div class="formula">c ≈ 1,079,252,848 km/h</div>
                    <p style="text-align: center;">This is the cosmic speed limit—nothing can go faster!</p>
                </div>
                
                <h3>The Time Dilation Formula</h3>
                <div class="formula-box">
                    <p><strong>The Lorentz Factor (γ):</strong></p>
                    <div class="formula">γ = 1 / √(1 - v²/c²)</div>
                    <br>
                    <p><strong>Time Dilation:</strong></p>
                    <div class="formula">Δt = γ × Δt₀</div>
                    <br>
                    <p style="text-align: center;">
                        Where:<br>
                        • v = velocity of the moving object<br>
                        • c = speed of light<br>
                        • Δt₀ = time experienced by the moving observer<br>
                        • Δt = time measured by the stationary observer<br>
                        • γ (gamma) = time dilation factor
                    </p>
                </div>
                
                <h3>Why Does This Happen?</h3>
                <p>Space and time are not separate—they form a four-dimensional fabric called spacetime. When you move through space, you're also moving through time. The faster you move through space, the slower you move through time. This keeps the speed of light constant for all observers, which is a fundamental law of physics.</p>
                
                <div class="info-card">
                    <h3>Important Reality Check:</h3>
                    <p><strong>You cannot actually "travel back in time" using speed.</strong> Time dilation only causes time to pass more slowly for the moving object—it still moves forward. The traveling twin ages less, but doesn't go backward in time. True backward time travel remains purely theoretical and faces severe scientific obstacles.</p>
                </div>

                <h3>Time Travel by Speed: Forward Only</h3>
                <p>In the context of special relativity, accelerating an object to high speeds (close to the speed of light) enables a form of "time travel" into the future. This occurs because of time dilation: from the perspective of a stationary observer, the moving object's clock ticks slower. When the object returns, more time has elapsed for the observer than for the traveler.</p>
                
                <p>For instance, if an object travels at 99% the speed of light (v = 0.99c) for 1 year according to its own clock (proper time Δt₀ = 1 year), the Lorentz factor γ ≈ 7.09. Thus, the stationary observer measures Δt = γ × Δt₀ ≈ 7.09 years. The traveler has effectively "jumped" 6.09 years into Earth's future upon return.</p>
                
                <div class="formula-box">
                    <p><strong>Forward Time Jump Formula:</strong></p>
                    <div class="formula">Time Jump = (γ - 1) × Δt₀</div>
                    <p style="text-align: center; font-size: 0.9em;">This quantifies how much "future" the traveler skips relative to the stationary frame.</p>
                </div>
                
                <p>However, this is strictly one-directional forward travel. Backward time travel would require velocities exceeding c, which violates causality and the principles of relativity. No known mechanism in special relativity allows reversal of time's arrow through speed alone. Concepts like wormholes or exotic matter (from general relativity) are speculative and unproven for backward travel.</p>
                
                <div class="info-card warning">
                    <h3>Implications for Interstellar Travel:</h3>
                    <p>At 99.999% c (γ ≈ 223.6), a 10-year journey (traveler time) could span over 2,236 years on Earth. Explorers might return to a future civilization, but they'd leave their era behind forever—no returning to "fix" the past.</p>
                </div>
                
                <h3>What About Speeds Below Light Speed?</h3>
                <div class="equation">At 10% light speed (0.1c): γ ≈ 1.005 (0.5% difference)</div>
                <div class="equation">At 50% light speed (0.5c): γ ≈ 1.155 (15.5% difference)</div>
                <div class="equation">At 90% light speed (0.9c): γ ≈ 2.294 (129% difference)</div>
                <div class="equation">At 99% light speed (0.99c): γ ≈ 7.089 (609% difference)</div>
                <div class="equation">At 99.9% light speed (0.999c): γ ≈ 22.366 (2,236% difference)</div>
                
                <h3>Experimental Confirmation</h3>
                <div class="info-card">
                    <p><strong>Muon Decay:</strong> Cosmic ray muons created in the upper atmosphere live only 2.2 microseconds. At near-light speeds, time dilation allows them to reach Earth's surface before decaying—something impossible without time dilation.</p>
                    <p><strong>Atomic Clocks:</strong> Atomic clocks flown on airplanes show measurable time differences compared to ground clocks, exactly as predicted by relativity.</p>
                    <p><strong>GPS Satellites:</strong> GPS systems must account for both special and general relativistic effects. Without these corrections, GPS would be off by kilometers!</p>
                </div>
            </div>
        </div>
        
        <!-- CALCULATOR TAB -->
        <div id="calculator" class="tab-content">
            <div class="section">
                <h2>Relativistic Calculators</h2>
                
                <div class="calculator">
                    <div>
                        <h3>Time Dilation Calculator</h3>
                        <div class="control-group">
                            <label>Enter velocity as % of light speed:</label>
                            <input type="number" id="timeVelocity" min="0" max="99.99" step="0.01" value="50">
                            <label>Time experienced by traveler (years):</label>
                            <input type="number" id="properTime" min="0" step="0.1" value="1">
                            <button onclick="calculateTimeDilation()">Calculate</button>
                        </div>
                        <div class="result-box" id="timeResult">
                            <div>Enter values and click Calculate</div>
                        </div>
                    </div>
                    
                    <div>
                        <h3>Relativistic Mass Calculator</h3>
                        <div class="control-group">
                            <label>Rest mass (kg):</label>
                            <input type="number" id="restMass" min="0" step="0.01" value="1000">
                            <label>Velocity (% of light speed):</label>
                            <input type="number" id="massVelocity" min="0" max="99.99" step="0.01" value="50">
                            <button onclick="calculateMass()">Calculate</button>
                        </div>
                        <div class="result-box" id="massResult">
                            <div>Enter values and click Calculate</div>
                        </div>
                        <div class="info-card">
                            <p><strong>Note:</strong> Relativistic mass increases with velocity according to m = γ × m₀</p>
                        </div>
                    </div>
                </div>
                
                <div class="calculator">
                    <div>
                        <h3>Length Contraction Calculator</h3>
                        <div class="control-group">
                            <label>Proper length (meters):</label>
                            <input type="number" id="properLength" min="0" step="1" value="100">
                            <label>Velocity (% of light speed):</label>
                            <input type="number" id="lengthVelocity" min="0" max="99.99" step="0.01" value="90">
                            <button onclick="calculateLength()">Calculate</button>
                        </div>
                        <div class="result-box" id="lengthResult">
                            <div>Enter values and click Calculate</div>
                        </div>
                        <div class="info-card">
                            <p><strong>Length Contraction:</strong> Objects appear shorter in the direction of motion: L = L₀ / γ</p>
                        </div>
                    </div>
                    
                    <div>
                        <h3>Relativistic Velocity Calculator</h3>
                        <div class="control-group">
                            <label>Desired γ (gamma) factor:</label>
                            <input type="number" id="desiredGamma" min="1" step="0.1" value="2">
                            <button onclick="calculateVelocity()">Calculate Required Velocity</button>
                        </div>
                        <div class="result-box" id="velocityResult">
                            <div>Enter values and click Calculate</div>
                        </div>
                        <div class="info-card">
                            <p>This calculates what velocity is needed to achieve a specific time dilation factor</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- EXAMPLES TAB -->
        <div id="examples" class="tab-content">
            <div class="section">
                <h2>Real-World Examples & Scenarios</h2>
                
                <div class="info-card">
                    <h3>Example 1: A Trip to Alpha Centauri</h3>
                    <p><strong>Distance:</strong> 4.37 light-years</p>
                    <p><strong>Travel Speed:</strong> 90% light speed (0.9c)</p>
                    <p><strong>For people on Earth:</strong> The trip takes 4.37 / 0.9 ≈ 4.86 years</p>
                    <p><strong>For the astronauts:</strong> Due to time dilation (γ ≈ 2.29), they only experience 4.86 / 2.29 ≈ 2.12 years</p>
                    <p><strong>Result:</strong> The astronauts age 2.74 years less than people on Earth!</p>
                </div>
                
                <div class="info-card">
                    <h3>Example 2: GPS Satellites</h3>
                    <p>GPS satellites orbit at about 20,000 km altitude and move at about 14,000 km/h</p>
                    <p><strong>Time dilation effect:</strong> Clocks on GPS satellites run about 7 microseconds per day SLOWER than Earth clocks</p>
                    <p><strong>Practical impact:</strong> Without correcting for this, GPS would accumulate errors of about 10 km per day!</p>
                </div>
                
                <div class="info-card">
                    <h3>Example 3: Particle Accelerators</h3>
                    <p>At CERN's Large Hadron Collider, protons travel at 99.9999991% the speed of light</p>
                    <p><strong>Time dilation factor:</strong> γ ≈ 7,453</p>
                    <p><strong>Meaning:</strong> For every second that passes for the proton, about 7,453 seconds (over 2 hours) pass for us!</p>
                </div>
                
                <div class="info-card">
                    <h3>Example 4: Hypothetical Interstellar Journey</h3>
                    <p><strong>Destination:</strong> Center of Milky Way (26,000 light-years away)</p>
                    <p><strong>Travel Speed:</strong> 99.9% light speed</p>
                    <p><strong>Earth perspective:</strong> ~26,000 years</p>
                    <p><strong>Traveler perspective:</strong> With γ ≈ 22.4, only about 1,160 years experienced</p>
                    <p><strong>Note:</strong> The traveler still can't return to "the past"—Earth has aged 26,000 years when they arrive.</p>
                </div>
                
                <div class="info-card warning">
                    <h3>The Energy Problem</h3>
                    <p>Reaching near-light speeds requires enormous energy. To accelerate 1 kg to:</p>
                    <div class="equation">50% light speed: ~10¹⁶ joules (≈ 3 nuclear bombs)</div>
                    <div class="equation">90% light speed: ~10¹⁷ joules (≈ 25 nuclear bombs)</div>
                    <div class="equation">99.9% light speed: ~10¹⁸ joules (≈ world's annual energy consumption)</div>
                    <p>This is why practical near-light-speed travel remains far beyond current technology.</p>
                </div>
            </div>
        </div>
    </div>

    <div class="watermark">
        <a href="https://www.instagram.com/rajput_anmolsingh3/" target="_blank">ANMOL SINGH/IG=rajput_anmolsingh3</a>
    </div>

    <script>
        const canvas = document.getElementById('timeCanvas');
        const ctx = canvas.getContext('2d');
        const c = 299792.458; // speed of light in km/s
        
        let earthTime = 0;
        let shipTime = 0;
        let velocity = 0;
        let gamma = 1;
        let animationRunning = false;
        let animationId;
        let shipX = 100;
        
        function showTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(tabName).classList.add('active');
            event.target.classList.add('active');
        }
        
        function calculateGamma(v) {
            if (v >= 1) return Infinity;
            return 1 / Math.sqrt(1 - (v * v));
        }
        
        document.getElementById('speedSlider').addEventListener('input', function() {
            const speedPercent = this.value;
            velocity = speedPercent / 100;
            gamma = calculateGamma(velocity);
            
            document.getElementById('speedPercent').textContent = speedPercent;
            document.getElementById('speedKmh').textContent = (velocity * c * 3600).toFixed(0).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
            document.getElementById('gamma').textContent = gamma.toFixed(3);
            document.getElementById('earthTime').textContent = gamma.toFixed(2);
        });
        
        function drawScene() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // Draw Earth
            ctx.fillStyle = '#4fc3f7';
            ctx.beginPath();
            ctx.arc(100, 200, 40, 0, Math.PI * 2);
            ctx.fill();
            ctx.fillStyle = 'white';
            ctx.font = 'bold 16px Arial';
            ctx.textAlign = 'center';
            ctx.fillText('Earth', 100, 260);
            
            // Draw spaceship
            ctx.fillStyle = '#ff6b6b';
            ctx.beginPath();
            ctx.moveTo(shipX, 200);
            ctx.lineTo(shipX + 30, 185);
            ctx.lineTo(shipX + 60, 185);
            ctx.lineTo(shipX + 70, 200);
            ctx.lineTo(shipX + 60, 215);
            ctx.lineTo(shipX + 30, 215);
            ctx.closePath();
            ctx.fill();
            
            // Draw trail
            if (velocity > 0) {
                ctx.strokeStyle = 'rgba(255,107,107,0.3)';
                ctx.lineWidth = 3;
                ctx.beginPath();
                ctx.moveTo(100, 200);
                ctx.lineTo(shipX, 200);
                ctx.stroke();
            }
            
            // Draw speed indicator
            ctx.fillStyle = 'white';
            ctx.font = '14px Arial';
            ctx.fillText(`v = ${(velocity * 100).toFixed(1)}% c`, shipX + 35, 240);
        }
        
        function updateClocks() {
            const earthMins = Math.floor(earthTime / 60);
            const earthSecs = Math.floor(earthTime % 60);
            const shipMins = Math.floor(shipTime / 60);
            const shipSecs = Math.floor(shipTime % 60);
            
            document.getElementById('earthClock').textContent = 
                `${String(earthMins).padStart(2, '0')}:${String(earthSecs).padStart(2, '0')}`;
            document.getElementById('shipClock').textContent = 
                `${String(shipMins).padStart(2, '0')}:${String(shipSecs).padStart(2, '0')}`;
        }
        
        function animate() {
            if (!animationRunning) return;
            
            earthTime += 0.05;
            shipTime += 0.05 / gamma;
            
            shipX += velocity * 2;
            if (shipX > canvas.width - 100) shipX = 100;
            
            drawScene();
            updateClocks();
            
            animationId = requestAnimationFrame(animate);
        }
        
        function startAnimation() {
            animationRunning = true;
            animate();
        }
        
        function pauseAnimation() {
            animationRunning = false;
            if (animationId) cancelAnimationFrame(animationId);
        }
        
        function resetAnimation() {
            pauseAnimation();
            earthTime = 0;
            shipTime = 0;
            shipX = 100;
            updateClocks();
            drawScene();
        }
        
        function calculateTimeDilation() {
            const v = parseFloat(document.getElementById('timeVelocity').value) / 100;
            const t0 = parseFloat(document.getElementById('properTime').value);
            const g = calculateGamma(v);
            const t = g * t0;
            const ageDiff = t - t0;
            
            document.getElementById('timeResult').innerHTML = `
                <h3>Results:</h3>
                <div>Lorentz Factor (γ): <span class="result-value">${g.toFixed(4)}</span></div>
                <div>Time on Earth: <span class="result-value">${t.toFixed(4)} years</span></div>
                <div>Age Difference: <span class="result-value">${ageDiff.toFixed(4)} years</span></div>
                <p>The traveler ages ${ageDiff.toFixed(2)} years less than people on Earth!</p>
            `;
        }
        
        function calculateMass() {
            const m0 = parseFloat(document.getElementById('restMass').value);
            const v = parseFloat(document.getElementById('massVelocity').value) / 100;
            const g = calculateGamma(v);
            const m = g * m0;
            const increase = m - m0;
            
            document.getElementById('massResult').innerHTML = `
                <h3>Results:</h3>
                <div>Rest Mass: <span class="result-value">${m0.toFixed(2)} kg</span></div>
                <div>Relativistic Mass: <span class="result-value">${m.toFixed(2)} kg</span></div>
                <div>Mass Increase: <span class="result-value">${increase.toFixed(2)} kg</span></div>
                <p>Mass increases by ${((increase/m0)*100).toFixed(1)}%</p>
            `;
        }
        
        function calculateLength() {
            const L0 = parseFloat(document.getElementById('properLength').value);
            const v = parseFloat(document.getElementById('lengthVelocity').value) / 100;
            const g = calculateGamma(v);
            const L = L0 / g;
            const contraction = L0 - L;
            
            document.getElementById('lengthResult').innerHTML = `
                <h3>Results:</h3>
                <div>Proper Length: <span class="result-value">${L0.toFixed(2)} m</span></div>
                <div>Contracted Length: <span class="result-value">${L.toFixed(2)} m</span></div>
                <div>Contraction: <span class="result-value">${contraction.toFixed(2)} m</span></div>
                <p>Length contracts by ${((contraction/L0)*100).toFixed(1)}%</p>
            `;
        }
        
        function calculateVelocity() {
            const g = parseFloat(document.getElementById('desiredGamma').value);
            if (g < 1) {
                document.getElementById('velocityResult').innerHTML = `
                    <div style="color: #ff9800;">γ must be ≥ 1</div>
                `;
                return;
            }
            
            const vSquared = 1 - (1 / (g * g));
            const v = Math.sqrt(vSquared);
            const vPercent = v * 100;
            const vKmh = v * c * 3600;
            
            document.getElementById('velocityResult').innerHTML = `
                <h3>Results:</h3>
                <div>Required Velocity: <span class="result-value">${vPercent.toFixed(2)}%</span> of light speed</div>
                <div>That's: <span class="result-value">${vKmh.toFixed(0).replace(/\B(?=(\d{3})+(?!\d))/g, ",")} km/h</span></div>
                <p>At this speed, time dilation factor is ${g.toFixed(2)}</p>
            `;
        }
        
        drawScene();
        updateClocks();
    </script>
</body>
</html>
