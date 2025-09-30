[focus_timer_web_app-2.html](https://github.com/user-attachments/files/22612644/focus_timer_web_app-2.html)

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Focus Timer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            overflow: hidden;
            position: relative;
        }

        .background-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }

        .base-gradient {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #1e3a8a 0%, #0f172a 100%);
        }

        .wave {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.7;
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.6) 0%, rgba(29, 78, 216, 0.5) 100%);
            animation: wave1 15s ease-in-out infinite;
            transform-origin: center;
        }

        .wave2 {
            opacity: 0.6;
            background: linear-gradient(135deg, rgba(37, 99, 235, 0.5) 0%, rgba(59, 130, 246, 0.7) 100%);
            animation: wave2 20s ease-in-out infinite reverse;
        }

        .wave3 {
            opacity: 0.4;
            background: linear-gradient(45deg, rgba(147, 197, 253, 0.4) 0%, rgba(59, 130, 246, 0.6) 100%);
            animation: wave3 25s ease-in-out infinite;
        }

        @keyframes wave1 {
            0%, 100% { 
                transform: translateX(0) translateY(0) scale(1) rotate(0deg);
                border-radius: 0% 0% 0% 0%;
            }
            25% { 
                transform: translateX(40px) translateY(-30px) scale(1.05) rotate(2deg);
                border-radius: 40% 50% 35% 60%;
            }
            50% { 
                transform: translateX(-20px) translateY(20px) scale(0.95) rotate(0deg);
                border-radius: 60% 35% 50% 40%;
            }
            75% { 
                transform: translateX(-50px) translateY(-10px) scale(1.03) rotate(-2deg);
                border-radius: 35% 60% 40% 50%;
            }
        }

        @keyframes wave2 {
            0%, 100% { 
                transform: translateX(0) translateY(0) scale(1) rotate(0deg);
                border-radius: 0% 0% 0% 0%;
            }
            33% { 
                transform: translateX(-30px) translateY(40px) scale(1.08) rotate(-2deg);
                border-radius: 50% 40% 60% 35%;
            }
            66% { 
                transform: translateX(50px) translateY(-20px) scale(0.92) rotate(2deg);
                border-radius: 40% 60% 35% 50%;
            }
        }

        @keyframes wave3 {
            0%, 100% { 
                transform: translateX(0) translateY(0) scale(1) rotate(0deg);
                border-radius: 0% 0% 0% 0%;
            }
            40% { 
                transform: translateX(20px) translateY(50px) scale(1.04) rotate(1deg);
                border-radius: 35% 50% 40% 60%;
            }
            80% { 
                transform: translateX(-40px) translateY(-30px) scale(0.96) rotate(-1deg);
                border-radius: 60% 40% 50% 35%;
            }
        }

        .app-container {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 24px;
            padding: 40px 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            text-align: center;
            min-width: 320px;
            max-width: 400px;
            width: 100%;
            z-index: 1;
        }

        .app-title {
            font-size: 28px;
            font-weight: 700;
            color: #2d3748;
            margin-bottom: 40px;
            letter-spacing: -0.5px;
        }

        .timer-display {
            font-size: 72px;
            font-weight: 300;
            color: #4a5568;
            margin-bottom: 40px;
            font-variant-numeric: tabular-nums;
            letter-spacing: -2px;
            transition: color 0.3s ease;
        }

        .timer-display.finished {
            color: #ff6b6b;
            animation: flash 1s ease-in-out;
        }

        @keyframes flash {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .controls {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-bottom: 30px;
        }

        .btn {
            padding: 16px 32px;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
            text-transform: none;
            letter-spacing: 0.5px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
        }

        .btn:active {
            transform: translateY(0);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }

        .timer-btn {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
        }

        .timer-btn.stop {
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a52 100%);
        }

        .reset-btn {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.8) 0%, rgba(255, 255, 255, 0.6) 100%);
            color: #2d3748;
            font-size: 16px;
            font-weight: 500;
            padding: 12px 32px;
            border: 1px solid rgba(0, 0, 0, 0.1);
        }

        .audio-section {
            margin: 20px 0;
            padding: 15px;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 12px;
            border: 1px solid rgba(0, 0, 0, 0.05);
        }

        .audio-file-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            font-size: 12px;
            color: #718096;
        }

        .audio-file-name {
            flex: 1;
            text-align: left;
            color: #4a5568;
            font-weight: 500;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .change-btn {
            background: none;
            border: none;
            color: #3182ce;
            font-size: 12px;
            font-weight: 600;
            cursor: pointer;
            padding: 4px 8px;
            border-radius: 4px;
            transition: background-color 0.2s;
        }

        .change-btn:hover {
            background: rgba(49, 130, 206, 0.1);
        }

        .file-input {
            display: none;
        }

        .audio-btn {
            background: linear-gradient(135deg, #a8e6cf 0%, #7fcdcd 100%);
            color: #2d3748;
        }

        .audio-btn.playing {
            background: linear-gradient(135deg, #ffd93d 0%, #ff6b6b 100%);
            color: white;
        }

        .audio-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }

        .status {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            font-size: 14px;
            color: #718096;
            margin-top: 20px;
        }

        .indicator {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #cbd5e0;
            transition: all 0.3s ease;
        }

        .indicator.active {
            background: #48bb78;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(1.2); }
        }

        .wave-animation {
            position: absolute;
            right: 16px;
            top: 50%;
            transform: translateY(-50%);
            display: flex;
            gap: 2px;
        }

        .wave-bar {
            width: 3px;
            height: 12px;
            background: rgba(255, 255, 255, 0.7);
            border-radius: 2px;
            animation: wave-bar 1.5s infinite ease-in-out;
        }

        .wave-bar:nth-child(2) { animation-delay: 0.1s; }
        .wave-bar:nth-child(3) { animation-delay: 0.2s; }
        .wave-bar:nth-child(4) { animation-delay: 0.3s; }

        @keyframes wave-bar {
            0%, 40%, 100% { transform: scaleY(0.4); }
            20% { transform: scaleY(1); }
        }

        .loading {
            display: inline-block;
            width: 12px;
            height: 12px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s linear infinite;
            margin-right: 8px;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        @media (max-width: 480px) {
            .app-container {
                padding: 30px 20px;
                margin: 10px;
            }
            
            .timer-display {
                font-size: 60px;
            }
            
            .btn {
                font-size: 16px;
                padding: 14px 28px;
            }
        }
    </style>
</head>
<body>
    <div class="background-container">
        <div class="base-gradient"></div>
        <div class="wave"></div>
        <div class="wave wave2"></div>
        <div class="wave wave3"></div>
    </div>

    <div class="app-container">
        <h1 class="app-title">Focus Timer</h1>
        
        <div class="timer-display" id="timerDisplay">60:00</div>
        
        <div class="controls">
            <button class="btn timer-btn" id="timerBtn" onclick="toggleTimer()">
                Start Timer
            </button>
            
            <button class="btn reset-btn" id="resetBtn" onclick="resetTimer()">
                Reset Timer
            </button>
            
            <div class="audio-section">
                <div class="audio-file-info">
                    <span style="font-weight: 600;">Current Audio:</span>
                </div>
                <div class="audio-file-info">
                    <span class="audio-file-name" id="audioFileName">Generated Ambient Sound</span>
                    <button class="change-btn" onclick="document.getElementById('audioFile').click()">Change</button>
                </div>
                <input type="file" id="audioFile" class="file-input" accept="audio/*" onchange="loadAudioFile(event)">
            </div>
            
            <button class="btn audio-btn" id="audioBtn" onclick="toggleAudio()">
                <span id="audioButtonText">Play Audio</span>
                <div class="wave-animation" id="waveAnimation" style="display: none;">
                    <div class="wave-bar"></div>
                    <div class="wave-bar"></div>
                    <div class="wave-bar"></div>
                    <div class="wave-bar"></div>
                </div>
            </button>
        </div>
        
        <div class="status">
            <div class="indicator" id="indicator"></div>
            <span id="statusText">Ready to focus</span>
        </div>
    </div>

    <script>
        let timerInterval;
        let timeRemaining = 3600; // 60 minutes in seconds
        let isTimerRunning = false;
        let isAudioPlaying = false;
        let isAudioLoading = false;
        let audioContext;
        let audioSource;
        let gainNode;
        let audioBuffer;
        let customAudioBuffer;

        function formatTime(seconds) {
            const minutes = Math.floor(seconds / 60);
            const remainingSeconds = seconds % 60;
            return `${minutes}:${remainingSeconds.toString().padStart(2, '0')}`;
        }

        function updateDisplay() {
            document.getElementById('timerDisplay').textContent = formatTime(timeRemaining);
        }

        function updateStatus() {
            const statusText = document.getElementById('statusText');
            const indicator = document.getElementById('indicator');
            
            if (timeRemaining <= 0) {
                statusText.textContent = "Time's up!";
                indicator.classList.remove('active');
            } else if (isTimerRunning && isAudioPlaying) {
                statusText.textContent = 'Timer running with audio';
                indicator.classList.add('active');
            } else if (isTimerRunning) {
                statusText.textContent = 'Timer running';
                indicator.classList.add('active');
            } else if (isAudioPlaying) {
                statusText.textContent = 'Audio playing';
                indicator.classList.add('active');
            } else if (isAudioLoading) {
                statusText.textContent = 'Loading audio...';
                indicator.classList.remove('active');
            } else {
                statusText.textContent = 'Ready to focus';
                indicator.classList.remove('active');
            }
        }

        function toggleTimer() {
            const btn = document.getElementById('timerBtn');

            if (isTimerRunning) {
                // Stop timer
                clearInterval(timerInterval);
                isTimerRunning = false;
                btn.textContent = 'Start Timer';
                btn.classList.remove('stop');
            } else {
                // Start timer
                isTimerRunning = true;
                btn.textContent = 'Stop Timer';
                btn.classList.add('stop');
                
                timerInterval = setInterval(() => {
                    timeRemaining--;
                    updateDisplay();
                    updateStatus();
                    
                    if (timeRemaining <= 0) {
                        // Timer finished
                        clearInterval(timerInterval);
                        isTimerRunning = false;
                        btn.textContent = 'Start Timer';
                        btn.classList.remove('stop');
                        
                        // Flash the display
                        document.getElementById('timerDisplay').classList.add('finished');
                        setTimeout(() => {
                            document.getElementById('timerDisplay').classList.remove('finished');
                        }, 1000);
                        
                        // Play gentle completion chime
                        playCompletionChime();
                        
                        // Reset timer
                        timeRemaining = 3600;
                        updateDisplay();
                        updateStatus();
                        
                        // Vibrate if supported
                        if (navigator.vibrate) {
                            navigator.vibrate([200, 100, 200]);
                        }
                    }
                }, 1000);
            }
            updateStatus();
        }

        function resetTimer() {
            // Stop timer if running
            clearInterval(timerInterval);
            isTimerRunning = false;
            
            // Reset display and buttons
            timeRemaining = 3600;
            updateDisplay();
            
            const timerBtn = document.getElementById('timerBtn');
            timerBtn.textContent = 'Start Timer';
            timerBtn.classList.remove('stop');
            
            updateStatus();
        }

        async function initAudioContext() {
            if (!audioContext) {
                audioContext = new (window.AudioContext || window.webkitAudioContext)();
                gainNode = audioContext.createGain();
                gainNode.connect(audioContext.destination);
                gainNode.gain.setValueAtTime(0.2, audioContext.currentTime); // Gentler volume
                
                // Create gentle ambient sound
                await createGentleAmbientSound();
            }
        }

        async function createGentleAmbientSound() {
            if (!audioContext) return;
            
            const sampleRate = audioContext.sampleRate;
            const duration = 3; // 3 seconds
            const frameCount = sampleRate * duration;
            
            audioBuffer = audioContext.createBuffer(1, frameCount, sampleRate);
            const channelData = audioBuffer.getChannelData(0);
            
            // Generate gentle ambient sound with layered sine waves
            for (let i = 0; i < frameCount; i++) {
                const t = i / sampleRate;
                
                // Layer multiple low-frequency sine waves for gentle ambient sound
                const wave1 = Math.sin(2 * Math.PI * 60 * t) * 0.03;   // Very low frequency
                const wave2 = Math.sin(2 * Math.PI * 120 * t) * 0.02;  // Low frequency  
                const wave3 = Math.sin(2 * Math.PI * 200 * t) * 0.015; // Mid-low frequency
                
                // Add very gentle noise
                const noise = (Math.random() - 0.5) * 0.02;
                
                let sample = wave1 + wave2 + wave3 + noise;
                
                // Apply gentle fade in/out to avoid clicks
                const fadeFrames = frameCount * 0.1;
                if (i < fadeFrames) {
                    sample *= i / fadeFrames;
                } else if (i > frameCount - fadeFrames) {
                    sample *= (frameCount - i) / fadeFrames;
                }
                
                channelData[i] = sample;
            }
        }

        async function createGentleChime() {
            if (!audioContext) return;
            
            const sampleRate = audioContext.sampleRate;
            const duration = 3; // 3 seconds for gentle fade out
            const frameCount = sampleRate * duration;
            
            const chimeBuffer = audioContext.createBuffer(1, frameCount, sampleRate);
            const channelData = chimeBuffer.getChannelData(0);
            
            // Generate gentle chime sound with harmonious frequencies
            for (let i = 0; i < frameCount; i++) {
                const t = i / sampleRate;
                
                // Beautiful harmonic frequencies for a peaceful chime
                const fundamental = Math.sin(2 * Math.PI * 523.25 * t) * 0.4;  // C5 note
                const harmonic1 = Math.sin(2 * Math.PI * 659.25 * t) * 0.3;   // E5 note
                const harmonic2 = Math.sin(2 * Math.PI * 783.99 * t) * 0.2;   // G5 note
                const harmonic3 = Math.sin(2 * Math.PI * 1046.50 * t) * 0.1;  // C6 note (octave)
                
                let sample = fundamental + harmonic1 + harmonic2 + harmonic3;
                
                // Create gentle exponential decay for natural chime fade-out
                const decay = Math.exp(-t * 1.5); // Gentle decay
                sample *= decay;
                
                // Apply gentle attack envelope (quick fade-in to avoid click)
                const attackFrames = sampleRate * 0.01; // 10ms attack
                if (i < attackFrames) {
                    sample *= i / attackFrames;
                }
                
                channelData[i] = sample * 0.3; // Overall gentle volume
            }
            
            return chimeBuffer;
        }

        async function playCompletionChime() {
            try {
                await initAudioContext();
                
                if (audioContext.state === 'suspended') {
                    await audioContext.resume();
                }
                
                const chimeBuffer = await createGentleChime();
                if (!chimeBuffer) return;
                
                // Create a separate gain node for the chime
                const chimeGain = audioContext.createGain();
                chimeGain.connect(audioContext.destination);
                chimeGain.gain.setValueAtTime(0.6, audioContext.currentTime); // Slightly louder than ambient
                
                const chimeSource = audioContext.createBufferSource();
                chimeSource.buffer = chimeBuffer;
                chimeSource.connect(chimeGain);
                
                chimeSource.start();
                
            } catch (error) {
                console.error('Error playing completion chime:', error);
            }
        }

        function loadAudioFile(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            isAudioLoading = true;
            updateAudioButton();
            updateStatus();
            
            const reader = new FileReader();
            reader.onload = async function(e) {
                try {
                    await initAudioContext();
                    
                    if (audioContext.state === 'suspended') {
                        await audioContext.resume();
                    }
                    
                    const arrayBuffer = e.target.result;
                    customAudioBuffer = await audioContext.decodeAudioData(arrayBuffer);
                    
                    document.getElementById('audioFileName').textContent = file.name;
                    
                } catch (error) {
                    console.error('Error loading audio file:', error);
                    document.getElementById('audioFileName').textContent = 'Error loading file';
                } finally {
                    isAudioLoading = false;
                    updateAudioButton();
                    updateStatus();
                }
            };
            
            reader.onerror = function() {
                isAudioLoading = false;
                updateAudioButton();
                updateStatus();
                document.getElementById('audioFileName').textContent = 'Error loading file';
            };
            
            reader.readAsArrayBuffer(file);
        }

        function updateAudioButton() {
            const btn = document.getElementById('audioBtn');
            const buttonText = document.getElementById('audioButtonText');
            const waveAnimation = document.getElementById('waveAnimation');
            
            if (isAudioLoading) {
                buttonText.innerHTML = '<span class="loading"></span>Loading Audio...';
                btn.disabled = true;
                waveAnimation.style.display = 'none';
                btn.classList.remove('playing');
            } else if (isAudioPlaying) {
                buttonText.textContent = 'Stop Audio';
                btn.disabled = false;
                waveAnimation.style.display = 'flex';
                btn.classList.add('playing');
            } else {
                buttonText.textContent = 'Play Audio';
                btn.disabled = false;
                waveAnimation.style.display = 'none';
                btn.classList.remove('playing');
            }
        }

        async function toggleAudio() {
            if (isAudioPlaying) {
                stopAudio();
            } else {
                await startAudio();
            }
        }

        async function startAudio() {
            try {
                await initAudioContext();
                
                if (audioContext.state === 'suspended') {
                    await audioContext.resume();
                }
                
                // Use custom audio if loaded, otherwise use generated ambient sound
                const bufferToPlay = customAudioBuffer || audioBuffer;
                if (!bufferToPlay) {
                    console.error('No audio buffer available');
                    return;
                }
                
                audioSource = audioContext.createBufferSource();
                audioSource.buffer = bufferToPlay;
                audioSource.loop = true;
                audioSource.connect(gainNode);
                
                audioSource.start();
                isAudioPlaying = true;
                
                updateAudioButton();
                updateStatus();
                
            } catch (error) {
                console.error('Error starting audio:', error);
            }
        }

        function stopAudio() {
            if (audioSource) {
                audioSource.stop();
                audioSource = null;
            }
            
            isAudioPlaying = false;
            updateAudioButton();
            updateStatus();
        }

        // Initialize display and create default audio
        updateDisplay();
        updateStatus();
        initAudioContext();
    </script>
</body>
</html>
