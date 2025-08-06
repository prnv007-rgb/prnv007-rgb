<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Arcade - Pranav R. Mallia</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Courier+Prime:wght@400;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: linear-gradient(135deg, #0a0a0a 0%, #1a0033 50%, #000011 100%);
            color: #00ffff;
            font-family: 'Orbitron', monospace;
            overflow-x: hidden;
            position: relative;
        }
        
        /* Animated background */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                radial-gradient(circle at 25% 25%, #ff00ff22 0%, transparent 50%),
                radial-gradient(circle at 75% 75%, #00ffff22 0%, transparent 50%);
            animation: pulse 4s ease-in-out infinite alternate;
            z-index: -1;
        }
        
        @keyframes pulse {
            0% { opacity: 0.3; }
            100% { opacity: 0.7; }
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        /* Neon glow effect */
        .neon {
            text-shadow: 
                0 0 5px currentColor,
                0 0 10px currentColor,
                0 0 15px currentColor,
                0 0 20px currentColor;
        }
        
        /* ASCII Art Header */
        .ascii-header {
            font-family: 'Courier Prime', monospace;
            font-size: clamp(8px, 1.5vw, 12px);
            line-height: 1;
            text-align: center;
            margin: 20px 0;
            color: #00ff00;
            white-space: pre;
            animation: flicker 3s linear infinite;
        }
        
        @keyframes flicker {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.8; }
            51% { opacity: 1; }
            52% { opacity: 0.9; }
            53% { opacity: 1; }
        }
        
        /* Insert Coin Animation */
        .insert-coin {
            text-align: center;
            margin: 30px 0;
            padding: 20px;
            border: 2px solid #ffff00;
            background: linear-gradient(45deg, #1a1a2e, #16213e);
            border-radius: 10px;
            position: relative;
            overflow: hidden;
        }
        
        .insert-coin::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, #ffff0033, transparent);
            animation: sweep 3s linear infinite;
        }
        
        @keyframes sweep {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .coin-text {
            position: relative;
            z-index: 2;
            font-size: 24px;
            font-weight: 900;
            animation: bounce 2s ease-in-out infinite;
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }
        
        /* Typing Animation */
        .typing-animation {
            font-size: 28px;
            text-align: center;
            margin: 30px 0;
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        /* Level Headers */
        .level-header {
            background: linear-gradient(45deg, #ff0080, #00ffff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-size: 32px;
            font-weight: 900;
            text-align: center;
            margin: 40px 0 20px;
            position: relative;
        }
        
        .level-header::before {
            content: '▲▼▲▼▲▼▲▼▲▼';
            position: absolute;
            top: -15px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 12px;
            color: #ffff00;
            animation: blink 1s infinite;
        }
        
        @keyframes blink {
            0%, 50% { opacity: 1; }
            51%, 100% { opacity: 0; }
        }
        
        /* Interactive Game Cards */
        .game-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        
        .game-card {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            border: 2px solid #00ffff;
            border-radius: 15px;
            padding: 20px;
            position: relative;
            cursor: pointer;
            transition: all 0.3s ease;
            overflow: hidden;
        }
        
        .game-card:hover {
            transform: translateY(-10px) scale(1.02);
            border-color: #ff00ff;
            box-shadow: 0 10px 30px rgba(255, 0, 255, 0.3);
        }
        
        .game-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }
        
        .game-card:hover::before {
            left: 100%;
        }
        
        .game-title {
            font-size: 20px;
            font-weight: 700;
            color: #00ff00;
            margin-bottom: 10px;
            text-align: center;
        }
        
        .game-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin: 15px 0;
        }
        
        .stat {
            text-align: center;
            padding: 8px;
            background: rgba(0, 255, 255, 0.1);
            border-radius: 8px;
            font-size: 12px;
        }
        
        .stat-value {
            display: block;
            font-size: 18px;
            font-weight: 700;
            color: #ffff00;
        }
        
        /* Tech Arsenal Badges */
        .tech-arsenal {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin: 30px 0;
        }
        
        .tech-badge {
            display: inline-block;
            padding: 8px 16px;
            background: linear-gradient(45deg, #ff0080, #00ffff);
            border-radius: 20px;
            font-size: 14px;
            font-weight: 700;
            color: #000;
            text-decoration: none;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .tech-badge:hover {
            transform: scale(1.1);
            animation: shake 0.5s ease-in-out;
        }
        
        @keyframes shake {
            0%, 100% { transform: translateX(0) scale(1.1); }
            25% { transform: translateX(-5px) scale(1.1); }
            75% { transform: translateX(5px) scale(1.1); }
        }
        
        /* Progress Bars */
        .progress-container {
            margin: 20px 0;
        }
        
        .progress-bar {
            width: 100%;
            height: 20px;
            background: #1a1a2e;
            border-radius: 10px;
            overflow: hidden;
            position: relative;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #00ff00, #ffff00, #ff0080);
            border-radius: 10px;
            position: relative;
            animation: progressPulse 2s ease-in-out infinite;
        }
        
        @keyframes progressPulse {
            0%, 100% { box-shadow: 0 0 10px rgba(0, 255, 0, 0.5); }
            50% { box-shadow: 0 0 20px rgba(255, 0, 128, 0.8); }
        }
        
        .progress-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-weight: 700;
            color: #000;
            z-index: 2;
        }
        
        /* Secret Room */
        .secret-room {
            background: linear-gradient(45deg, #2d1b69, #11998e);
            border: 3px solid #ffd700;
            border-radius: 15px;
            padding: 30px;
            margin: 40px 0;
            text-align: center;
            position: relative;
            cursor: pointer;
        }
        
        .secret-room:hover {
            animation: secretGlow 1s ease-in-out infinite alternate;
        }
        
        @keyframes secretGlow {
            0% { box-shadow: 0 0 20px #ffd700; }
            100% { box-shadow: 0 0 40px #ffd700, 0 0 60px #ffd700; }
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            .ascii-header {
                font-size: 8px;
            }
            
            .level-header {
                font-size: 24px;
            }
            
            .game-grid {
                grid-template-columns: 1fr;
            }
        }
        
        /* Interactive Elements */
        .clickable {
            cursor: pointer;
            user-select: none;
        }
        
        .health-bar {
            width: 200px;
            height: 10px;
            background: #333;
            border-radius: 5px;
            margin: 10px auto;
            overflow: hidden;
        }
        
        .health-fill {
            height: 100%;
            background: linear-gradient(90deg, #ff0000, #ffff00, #00ff00);
            width: 85%;
            animation: healthPulse 1.5s ease-in-out infinite;
        }
        
        @keyframes healthPulse {
            0%, 100% { width: 85%; }
            50% { width: 90%; }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- ASCII Header -->
        <div class="ascii-header neon">
╔══════════════════════════════════════════════════════════════════╗
║                        ⚡ AI ARCADE ⚡                          ║
╚══════════════════════════════════════════════════════════════════╝

██████╗ ██████╗  █████╗ ███╗   ██╗ █████╗ ██╗   ██╗
██╔══██╗██╔══██╗██╔══██╗████╗  ██║██╔══██╗██║   ██║
██████╔╝██████╔╝███████║██╔██╗ ██║███████║██║   ██║
██╔═══╝ ██╔══██╗██╔══██║██║╚██╗██║██╔══██║╚██╗ ██╔╝
██║     ██║  ██║██║  ██║██║ ╚████║██║  ██║ ╚████╔╝ 
╚═╝     ╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝  ╚═╝  ╚═══╝  

███╗   ███╗ █████╗ ██╗     ██╗     ██╗ █████╗ 
████╗ ████║██╔══██╗██║     ██║     ██║██╔══██╗
██╔████╔██║███████║██║     ██║     ██║███████║
██║╚██╔╝██║██╔══██║██║     ██║     ██║██╔══██║
██║ ╚═╝ ██║██║  ██║███████╗███████╗██║██║  ██║
╚═╝     ╚═╝╚═╝  ╚═╝╚══════╝╚══════╝╚═╝╚═╝  ╚═╝
        </div>

        <!-- Insert Coin -->
        <div class="insert-coin">
            <div class="coin-text neon">🪙 INSERT COIN TO START 🪙</div>
            <div style="margin-top: 10px; font-size: 14px;">🤖 AI + ML Developer • 🎯 Recommender Systems • 🧠 NLP & LLM Expert</div>
        </div>

        <!-- Typing Animation -->
        <div class="typing-animation">
            <div id="typing-text"></div>
        </div>

        <!-- Player Stats -->
        <div style="text-align: center; margin: 30px 0;">
            <div style="display: inline-block; margin: 0 20px;">
                <div style="font-size: 18px; color: #ff00ff;">❤️ HEALTH</div>
                <div class="health-bar">
                    <div class="health-fill"></div>
                </div>
                <div style="font-size: 12px;">85/100</div>
            </div>
        </div>

        <!-- Level 1: Tech Arsenal -->
        <div class="level-header">🔫 LEVEL 1: TECH ARSENAL</div>
        
        <div class="progress-container">
            <div class="progress-bar">
                <div class="progress-fill" style="width: 95%;">
                    <div class="progress-text">MASTERY: 95%</div>
                </div>
            </div>
        </div>

        <div class="tech-arsenal">
            <div class="tech-badge clickable" onclick="powerUp(this)">🐍 Python</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">🧠 TensorFlow</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">🔥 PyTorch</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">🤗 Hugging Face</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">⚡ FastAPI</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">⚛️ React</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">🎨 Tailwind</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">🔍 FAISS</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">🦙 LLaMA</div>
            <div class="tech-badge clickable" onclick="powerUp(this)">💎 Gemini</div>
        </div>

        <!-- Level 2: Project Lab -->
        <div class="level-header">🧪 LEVEL 2: PROJECT LAB</div>

        <div class="game-grid">
            <div class="game-card clickable" onclick="startQuest('hybrid-recommender')">
                <div class="game-title">🎯 HYBRID RECOMMENDER</div>
                <div class="game-stats">
                    <div class="stat">
                        <span class="stat-value">95%</span>
                        Accuracy
                    </div>
                    <div class="stat">
                        <span class="stat-value">3</span>
                        Datasets
                    </div>
                    <div class="stat">
                        <span class="stat-value">⚡</span>
                        Real-Time
                    </div>
                    <div class="stat">
                        <span class="stat-value">🏆</span>
                        SOTA
                    </div>
                </div>
                <div style="text-align: center; margin-top: 15px;">
                    <div style="font-size: 14px; color: #00ffff;">Classical + Embedding Fusion</div>
                    <div style="font-size: 12px; margin-top: 5px;">Yelp • MovieLens • Amazon</div>
                </div>
            </div>

            <div class="game-card clickable" onclick="startQuest('rag-chatbot')">
                <div class="game-title">🦙 RAG CHATBOT</div>
                <div class="game-stats">
                    <div class="stat">
                        <span class="stat-value">100%</span>
                        Deploy
                    </div>
                    <div class="stat">
                        <span class="stat-value">🧠</span>
                        LLaMA
                    </div>
                    <div class="stat">
                        <span class="stat-value">📚</span>
                        Docs
                    </div>
                    <div class="stat">
                        <span class="stat-value">💬</span>
                        Chat
                    </div>
                </div>
                <div style="text-align: center; margin-top: 15px;">
                    <div style="font-size: 14px; color: #00ffff;">Document Intelligence + RAG</div>
                    <div style="font-size: 12px; margin-top: 5px;">FAISS • Context • Real-time</div>
                </div>
            </div>

            <div class="game-card clickable" onclick="startQuest('emotion-ai')">
                <div class="game-title">🎭 EMOTION DETECTOR</div>
                <div class="game-stats">
                    <div class="stat">
                        <span class="stat-value">94.2%</span>
                        Precision
                    </div>
                    <div class="stat">
                        <span class="stat-value">🤖</span>
                        RoBERTa
                    </div>
                    <div class="stat">
                        <span class="stat-value">😄</span>
                        Multi
                    </div>
                    <div class="stat">
                        <span class="stat-value">🚀</span>
                        Ready
                    </div>
                </div>
                <div style="text-align: center; margin-top: 15px;">
                    <div style="font-size: 14px; color: #00ffff;">RoBERTa + CapsNet Fusion</div>
                    <div style="font-size: 12px; margin-top: 5px;">Fine-tuned • Production</div>
                </div>
            </div>

            <div class="game-card clickable" onclick="startQuest('ai-websites')">
                <div class="game-title">🌐 AI WEB PORTALS</div>
                <div class="game-stats">
                    <div class="stat">
                        <span class="stat-value">∞</span>
                        Scale
                    </div>
                    <div class="stat">
                        <span class="stat-value">⚛️</span>
                        React
                    </div>
                    <div class="stat">
                        <span class="stat-value">🎨</span>
                        Design
                    </div>
                    <div class="stat">
                        <span class="stat-value">🤖</span>
                        AI
                    </div>
                </div>
                <div style="text-align: center; margin-top: 15px;">
                    <div style="font-size: 14px; color: #00ffff;">Full-Stack AI Integration</div>
                    <div style="font-size: 12px; margin-top: 5px;">FastAPI • Tailwind • UX</div>
                </div>
            </div>
        </div>

        <!-- Level 3: Stats & Achievements -->
        <div class="level-header">📊 LEVEL 3: STATS & ACHIEVEMENTS</div>

        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; margin: 30px 0;">
            <div style="background: linear-gradient(45deg, #1a1a2e, #16213e); padding: 20px; border-radius: 15px; border: 2px solid #00ff00; text-align: center;">
                <div style="font-size: 32px; font-weight: 900; color: #00ff00;">25+</div>
                <div style="font-size: 14px;">🤖 AI Models Trained</div>
            </div>
            <div style="background: linear-gradient(45deg, #1a1a2e, #16213e); padding: 20px; border-radius: 15px; border: 2px solid #ffff00; text-align: center;">
                <div style="font-size: 32px; font-weight: 900; color: #ffff00;">9000+</div>
                <div style="font-size: 14px;">☕ Coffee Cups</div>
            </div>
            <div style="background: linear-gradient(45deg, #1a1a2e, #16213e); padding: 20px; border-radius: 15px; border: 2px solid #ff00ff; text-align: center;">
                <div style="font-size: 32px; font-weight: 900; color: #ff00ff;">∞</div>
                <div style="font-size: 14px;">🧠 Algorithms Mastered</div>
            </div>
            <div style="background: linear-gradient(45deg, #1a1a2e, #16213e); padding: 20px; border-radius: 15px; border: 2px solid #ffd700; text-align: center;">
                <div style="font-size: 32px; font-weight: 900; color: #ffd700;">42</div>
                <div style="font-size: 14px;">🏆 Boss Battles Won</div>
            </div>
        </div>

        <!-- Experience Points -->
        <div style="text-align: center; margin: 30px 0;">
            <div style="font-size: 24px; color: #ffd700; margin-bottom: 10px;">⭐ EXPERIENCE POINTS ⭐</div>
            <div class="progress-bar" style="max-width: 400px; margin: 0 auto;">
                <div class="progress-fill" style="width: 87%;">
                    <div class="progress-text">Level 87 - AI Grandmaster</div>
                </div>
            </div>
        </div>

        <!-- Level 4: Secret Room -->
        <div class="level-header">🔐 LEVEL 4: SECRET ROOM</div>

        <div class="secret-room clickable" onclick="unlockSecret()">
            <div style="font-size: 48px; margin-bottom: 20px;">🗝️</div>
            <div style="font-size: 24px; font-weight: 900; margin-bottom: 10px;">CLASSIFIED PROJECT</div>
            <div style="font-size: 16px; opacity: 0.8;">Click to unlock the hidden chamber...</div>
            <div id="secret-content" style="display: none; margin-top: 20px; padding: 20px; background: rgba(0,0,0,0.3); border-radius: 10px;">
                <div style="font-size: 20px; color: #ffd700; margin-bottom: 10px;">🎉 CONGRATULATIONS! 🎉</div>
                <div style="font-size: 14px;">You've discovered my secret research project:</div>
                <div style="font-size: 18px; color: #00ffff; margin: 10px 0; font-weight: 700;">Multi-Modal AI Fusion Engine</div>
                <div style="font-size: 12px;">Combining vision, text, and audio processing with quantum-inspired algorithms</div>
                <div style="margin-top: 15px;">
                    <span style="background: #ff00ff; color: #000; padding: 5px 10px; border-radius: 5px; font-size: 12px; font-weight: 700;">🚀 COMING SOON</span>
                </div>
            </div>
        </div>

        <!-- Multiplayer Mode -->
        <div style="text-align: center; margin: 40px 0; padding: 30px; background: linear-gradient(45deg, #0f3460, #16537e); border-radius: 15px; border: 2px solid #00ffff;">
            <div style="font-size: 28px; font-weight: 900; margin-bottom: 20px; color: #00ffff;">🎮 MULTIPLAYER MODE</div>
            <div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
                <a href="https://linkedin.com/in/pranavmallia" style="text-decoration: none; background: #0077b5; color: white; padding: 10px 20px; border-radius: 25px; font-weight: 700; transition: all 0.3s;" onmouseover="this.style.transform='scale(1.1)'" onmouseout="this.style.transform='scale(1)'">💼 LinkedIn</a>
                <a href="https://github.com/pranavmallia" style="text-decoration: none; background: #333; color: white; padding: 10px 20px; border-radius: 25px; font-weight: 700; transition: all 0.3s;" onmouseover="this.style.transform='scale(1.1)'" onmouseout="this.style.transform='scale(1)'">🐙 GitHub</a>
                <a href="mailto:pranav.mallia@example.com" style="text-decoration: none; background: #ea4335; color: white; padding: 10px 20px; border-radius: 25px; font-weight: 700; transition: all 0.3s;" onmouseover="this.style.transform='scale(1.1)'" onmouseout="this.style.transform='scale(1)'">📧 Email</a>
                <a href="https://pranavmallia.dev" style="text-decoration: none; background: #ff6b35; color: white; padding: 10px 20px; border-radius: 25px; font-weight: 700; transition: all 0.3s;" onmouseover="this.style.transform='scale(1.1)'" onmouseout="this.style.transform='scale(1)'">🌐 Portfolio</a>
            </div>
            <div style="margin-top: 20px; font-size: 14px; color: #00ffff;">
                🤝 <strong>CO-OP MISSIONS:</strong> AI Hackathons • ML Research • Code Reviews • Coffee Chats
            </div>
        </div>

        <!-- Game Over -->
        <div style="text-align: center; margin: 40px 0; font-size: 18px;">
            <div style="animation: blink 1s infinite;">🎮 THANKS FOR PLAYING! 🎮</div>
            <div style="margin-top: 10px; font-size: 14px; opacity: 0.7;">Press F5 to respawn</div>
        </div>
    </div>

    <script>
        // Typing animation
        const phrases = [
            "🤖 Initializing AI systems...",
            "🧠 Loading neural networks...", 
            "🎯 Calibrating recommenders...",
            "🔥 Deploying ML models...",
            "⚡ Ready to code the future!"
        ];
        
        let currentPhrase = 0;
        let currentChar = 0;
        let isDeleting = false;
        
        function typeWriter() {
            const element = document.getElementById('typing-text');
            const current = phrases[currentPhrase];
            
            if (isDeleting) {
                element.textContent = current.substring(0, currentChar - 1);
                currentChar--;
            } else {
                element.textContent = current.substring(0, currentChar + 1);
                currentChar++;
            }
            
            if (!isDeleting && currentChar === current.length) {
                setTimeout(() => isDeleting = true, 2000);
            } else if (isDeleting && currentChar === 0) {
                isDeleting = false;
                currentPhrase = (currentPhrase + 1) % phrases.length;
            }
            
            const speed = isDeleting ? 50 : 100;
            setTimeout(typeWriter, speed);
        }
        
        typeWriter();
        
        // Interactive functions
        function powerUp(element) {
            element.style.animation = 'shake 0.5s ease-in-out';
            element.style.background = 'linear-gradient(45deg, #ffd700, #ff6b35)';
            
            // Create floating +1 effect
            const floatingText = document.createElement('div');
            floatingText.textContent = '+1 SKILL';
            floatingText.style.cssText = `
                position: fixed;
                color: #00ff00;
                font-weight: bold;
                font-size: 14px;
                pointer-events: none;
                z-index: 1000;
                animation: float 2s ease-out forwards;
            `;
            
            const rect = element.getBoundingClientRect();
            floatingText.style.left = rect.left + rect.width/2 + 'px';
            floatingText.style.top = rect.top + 'px';
            
            document.body.appendChild(floatingText);
            
            setTimeout(() => {
                element.style.animation = '';
                element.style.background = 'linear-gradient(45deg, #ff0080, #00ffff)';
                document.body.removeChild(floatingText);
            }, 2000);
        }
        
        function startQuest(questName) {
            const quests = {
                'hybrid-recommender': {
                    title: '🎯 HYBRID RECOMMENDER QUEST',
                    description: 'Combining classical collaborative filtering with modern embedding techniques!',
                    reward: '+500 XP, Recommender Master Badge'
                },
                'rag-chatbot': {
                    title: '🦙 RAG CHATBOT QUEST',
                    description: 'Deploy intelligent document-aware chatbots with LLaMA and FAISS!',
                    reward: '+750 XP, NLP Wizard Title'
                },
                'emotion-ai': {
                    title: '🎭 EMOTION DETECTOR QUEST', 
                    description: 'Fine-tune RoBERTa for multi-emotion classification with 94.2% accuracy!',
                    reward: '+600 XP, Emotion Master Badge'
                },
                'ai-websites': {
                    title: '🌐 AI WEB PORTALS QUEST',
                    description: 'Build full-stack AI-powered web applications with React and FastAPI!',
                    reward: '+800 XP, Full-Stack AI Developer'
                }
            };
            
            const quest = quests[questName];
            if (quest) {
                const modal = document.createElement('div');
                modal.style.cssText = `
                    position: fixed;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    background: rgba(0,0,0,0.9);
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    z-index: 1000;
                    animation: fadeIn 0.3s ease;
                `;
                
                modal.innerHTML = `
                    <div style="
                        background: linear-gradient(135deg, #1a1a2e, #16213e);
                        border: 3px solid #00ffff;
                        border-radius: 20px;
                        padding: 40px;
                        max-width: 500px;
                        text-align: center;
                        position: relative;
                        animation: slideIn 0.5s ease;
                    ">
                        <div style="font-size: 28px; font-weight: 900; color: #00ffff; margin-bottom: 20px;">
                            ${quest.title}
                        </div>
                        <div style="font-size: 16px; margin-bottom: 20px; line-height: 1.6;">
                            ${quest.description}
                        </div>
                        <div style="background: rgba(255,215,0,0.2); padding: 15px; border-radius: 10px; margin: 20px 0;">
                            <div style="color: #ffd700; font-weight: 700;">🏆 QUEST REWARD:</div>
                            <div style="font-size: 14px; margin-top: 5px;">${quest.reward}</div>
                        </div>
                        <div style="display: flex; gap: 15px; justify-content: center; margin-top: 25px;">
                            <button onclick="acceptQuest('${questName}')" style="
                                background: linear-gradient(45deg, #00ff00, #00cc00);
                                border: none;
                                color: #000;
                                padding: 12px 25px;
                                border-radius: 25px;
                                font-weight: 700;
                                cursor: pointer;
                                font-size: 14px;
                                transition: all 0.3s;
                            ">⚔️ ACCEPT QUEST</button>
                            <button onclick="closeModal()" style="
                                background: linear-gradient(45deg, #ff0080, #cc0066);
                                border: none;
                                color: white;
                                padding: 12px 25px;
                                border-radius: 25px;
                                font-weight: 700;
                                cursor: pointer;
                                font-size: 14px;
                                transition: all 0.3s;
                            ">❌ CANCEL</button>
                        </div>
                        <button onclick="closeModal()" style="
                            position: absolute;
                            top: 15px;
                            right: 20px;
                            background: none;
                            border: none;
                            color: #00ffff;
                            font-size: 24px;
                            cursor: pointer;
                        ">×</button>
                    </div>
                `;
                
                document.body.appendChild(modal);
            }
        }
        
        function acceptQuest(questName) {
            closeModal();
            
            // Show quest accepted notification
            const notification = document.createElement('div');
            notification.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                background: linear-gradient(45deg, #00ff00, #00cc00);
                color: #000;
                padding: 15px 25px;
                border-radius: 15px;
                font-weight: 700;
                z-index: 1000;
                animation: slideInRight 0.5s ease, fadeOut 0.5s ease 3s forwards;
            `;
            notification.textContent = '🎉 QUEST ACCEPTED! Check GitHub for details.';
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                if (document.body.contains(notification)) {
                    document.body.removeChild(notification);
                }
            }, 3500);
        }
        
        function closeModal() {
            const modal = document.querySelector('div[style*="position: fixed"][style*="background: rgba(0,0,0,0.9)"]');
            if (modal) {
                modal.style.animation = 'fadeOut 0.3s ease';
                setTimeout(() => {
                    if (document.body.contains(modal)) {
                        document.body.removeChild(modal);
                    }
                }, 300);
            }
        }
        
        function unlockSecret() {
            const secretContent = document.getElementById('secret-content');
            if (secretContent.style.display === 'none') {
                secretContent.style.display = 'block';
                secretContent.style.animation = 'fadeIn 0.8s ease';
                
                // Add some particle effects
                createParticles();
                
                // Play unlock sound effect (visual representation)
                const soundEffect = document.createElement('div');
                soundEffect.textContent = '🔓 *UNLOCK SOUND* 🔓';
                soundEffect.style.cssText = `
                    position: fixed;
                    top: 50%;
                    left: 50%;
                    transform: translate(-50%, -50%);
                    color: #ffd700;
                    font-size: 24px;
                    font-weight: 900;
                    pointer-events: none;
                    z-index: 1000;
                    animation: pulse 0.5s ease, fadeOut 0.5s ease 1s forwards;
                `;
                
                document.body.appendChild(soundEffect);
                
                setTimeout(() => {
                    if (document.body.contains(soundEffect)) {
                        document.body.removeChild(soundEffect);
                    }
                }, 1500);
            }
        }
        
        function createParticles() {
            for (let i = 0; i < 20; i++) {
                const particle = document.createElement('div');
                particle.textContent = ['⭐', '💎', '🔥', '⚡', '✨'][Math.floor(Math.random() * 5)];
                particle.style.cssText = `
                    position: fixed;
                    font-size: 20px;
                    pointer-events: none;
                    z-index: 999;
                    animation: particle 3s ease-out forwards;
                `;
                
                particle.style.left = Math.random() * window.innerWidth + 'px';
                particle.style.top = Math.random() * window.innerHeight + 'px';
                
                document.body.appendChild(particle);
                
                setTimeout(() => {
                    if (document.body.contains(particle)) {
                        document.body.removeChild(particle);
                    }
                }, 3000);
            }
        }
        
        // Add CSS animations
        const style = document.createElement('style');
        style.textContent = `
            @keyframes float {
                0% { transform: translateY(0); opacity: 1; }
                100% { transform: translateY(-50px); opacity: 0; }
            }
            
            @keyframes fadeIn {
                0% { opacity: 0; }
                100% { opacity: 1; }
            }
            
            @keyframes fadeOut {
                0% { opacity: 1; }
                100% { opacity: 0; }
            }
            
            @keyframes slideIn {
                0% { transform: translateY(-50px); opacity: 0; }
                100% { transform: translateY(0); opacity: 1; }
            }
            
            @keyframes slideInRight {
                0% { transform: translateX(100px); opacity: 0; }
                100% { transform: translateX(0); opacity: 1; }
            }
            
            @keyframes particle {
                0% { 
                    transform: translateY(0) rotate(0deg) scale(1); 
                    opacity: 1; 
                }
                100% { 
                    transform: translateY(-200px) rotate(360deg) scale(0); 
                    opacity: 0; 
                }
            }
        `;
        document.head.appendChild(style);
        
        // Add click sound effects (visual feedback)
        document.addEventListener('click', function(e) {
            if (e.target.classList.contains('clickable')) {
                const ripple = document.createElement('div');
                ripple.style.cssText = `
                    position: absolute;
                    border-radius: 50%;
                    background: rgba(0, 255, 255, 0.3);
                    transform: scale(0);
                    animation: ripple 0.6s ease-out;
                    pointer-events: none;
                `;
                
                const rect = e.target.getBoundingClientRect();
                const size = Math.max(rect.width, rect.height);
                ripple.style.width = size + 'px';
                ripple.style.height = size + 'px';
                ripple.style.left = (e.clientX - rect.left - size/2) + 'px';
                ripple.style.top = (e.clientY - rect.top - size/2) + 'px';
                
                e.target.style.position = 'relative';
                e.target.appendChild(ripple);
                
                setTimeout(() => {
                    if (e.target.contains(ripple)) {
                        e.target.removeChild(ripple);
                    }
                }, 600);
            }
        });
        
        // Add ripple animation
        const rippleStyle = document.createElement('style');
        rippleStyle.textContent = `
            @keyframes ripple {
                to {
                    transform: scale(2);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(rippleStyle);
        
        // Easter egg: Konami code
        let konamiCode = [];
        const konamiSequence = ['ArrowUp', 'ArrowUp', 'ArrowDown', 'ArrowDown', 'ArrowLeft', 'ArrowRight', 'ArrowLeft', 'ArrowRight', 'KeyB', 'KeyA'];
        
        document.addEventListener('keydown', function(e) {
            konamiCode.push(e.code);
            if (konamiCode.length > konamiSequence.length) {
                konamiCode.shift();
            }
            
            if (JSON.stringify(konamiCode) === JSON.stringify(konamiSequence)) {
                // Activate cheat mode
                const cheatMessage = document.createElement('div');
                cheatMessage.innerHTML = `
                    <div style="font-size: 24px; margin-bottom: 10px;">🎮 CHEAT CODE ACTIVATED! 🎮</div>
                    <div style="font-size: 16px;">🚀 INFINITE LIVES ENABLED</div>
                    <div style="font-size: 16px;">⚡ ALL SKILLS MAXED OUT</div>
                    <div style="font-size: 16px;">🏆 GOD MODE: ON</div>
                `;
                cheatMessage.style.cssText = `
                    position: fixed;
                    top: 50%;
                    left: 50%;
                    transform: translate(-50%, -50%);
                    background: linear-gradient(45deg, #ff00ff, #00ffff);
                    color: #000;
                    padding: 30px;
                    border-radius: 20px;
                    text-align: center;
                    font-weight: 700;
                    z-index: 1000;
                    animation: pulse 1s ease-in-out infinite;
                `;
                
                document.body.appendChild(cheatMessage);
                
                // Change page colors to rainbow
                document.body.style.animation = 'rainbow 2s linear infinite';
                
                setTimeout(() => {
                    if (document.body.contains(cheatMessage)) {
                        document.body.removeChild(cheatMessage);
                    }
                    document.body.style.animation = '';
                }, 5000);
                
                konamiCode = [];
            }
        });
        
        // Add rainbow animation
        const rainbowStyle = document.createElement('style');
        rainbowStyle.textContent = `
            @keyframes rainbow {
                0% { filter: hue-rotate(0deg); }
                100% { filter: hue-rotate(360deg); }
            }
        `;
        document.head.appendChild(rainbowStyle);
    </script>
</body>
</html>
