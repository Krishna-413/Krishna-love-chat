<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multilingual Love Message Autoreply</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&family=Playfair+Display:wght@400;500;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #ff4d6d;
            --primary-dark: #c9184a;
            --secondary: #ff8fa3;
            --light: #fff0f3;
            --dark: #590d22;
            --accent: #ffccd5;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, var(--light), #f8f9fa);
            color: var(--dark);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(89, 13, 34, 0.1);
            width: 100%;
            max-width: 600px;
            padding: 30px;
            position: relative;
            overflow: hidden;
        }

        .container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 10px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
        }

        h1 {
            font-family: 'Playfair Display', serif;
            color: var(--primary-dark);
            margin-bottom: 15px;
            text-align: center;
            font-weight: 600;
            font-size: 28px;
        }

        .heart-container {
            display: flex;
            justify-content: center;
            margin: 20px 0;
        }

        .heart {
            font-size: 50px;
            color: var(--primary);
            animation: pulse 1.5s infinite;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .heart:hover {
            transform: scale(1.2);
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }

        .input-section {
            margin-bottom: 25px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }

        textarea, select {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid var(--accent);
            border-radius: 12px;
            font-family: 'Poppins', sans-serif;
            font-size: 16px;
            transition: all 0.3s;
            background-color: white;
        }

        textarea {
            min-height: 120px;
            resize: vertical;
        }

        textarea:focus, select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(255, 77, 109, 0.2);
        }

        .settings {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 25px;
        }

        @media (max-width: 480px) {
            .settings {
                grid-template-columns: 1fr;
            }
        }

        .btn-group {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
            margin-bottom: 25px;
        }

        button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 30px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 500;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        button:hover {
            background-color: var(--primary-dark);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(201, 24, 74, 0.3);
        }

        button:active {
            transform: translateY(0);
        }

        button.secondary {
            background-color: white;
            color: var(--primary);
            border: 2px solid var(--primary);
        }

        button.secondary:hover {
            background-color: var(--light);
        }

        .response-box {
            margin-top: 20px;
            padding: 20px;
            background-color: var(--light);
            border-radius: 15px;
            min-height: 150px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            line-height: 1.6;
            border: 1px dashed var(--secondary);
            transition: all 0.3s;
        }

        .response-box:hover {
            border-color: var(--primary);
        }

        .hidden {
            display: none;
        }

        .loading {
            font-style: italic;
            color: #6c757d;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .loading::after {
            content: '';
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255, 77, 109, 0.3);
            border-radius: 50%;
            border-top-color: var(--primary);
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .footer {
            margin-top: 30px;
            text-align: center;
            font-size: 14px;
            color: #6c757d;
        }

        .language-selector {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .lang-btn {
            padding: 8px 15px;
            font-size: 14px;
            border-radius: 20px;
            background-color: white;
            border: 1px solid #dee2e6;
            color: var(--dark);
            transition: all 0.3s;
        }

        .lang-btn:hover {
            background-color: #f8f9fa;
        }

        .lang-btn.active {
            background-color: var(--primary);
            color: white;
            border-color: var(--primary);
        }

        .floating-hearts {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
            overflow: hidden;
        }

        .floating-heart {
            position: absolute;
            opacity: 0;
            font-size: 20px;
            color: var(--secondary);
            animation: float 10s linear infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 0.7;
            }
            90% {
                opacity: 0.7;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="floating-hearts" id="floatingHearts"></div>
        
        <h1 id="appTitle">Love Message Autoreply</h1>
        
        <div class="language-selector">
            <button class="lang-btn active" data-lang="en">English</button>
            <button class="lang-btn" data-lang="hi">हिंदी</button>
            <button class="lang-btn" data-lang="kn">ಕನ್ನಡ</button>
            <button class="lang-btn" data-lang="te">తెలుగు</button>
        </div>
        
        <div class="heart-container">
            <div class="heart" id="heartBtn">❤️</div>
        </div>
        
        <div class="input-section">
            <label id="messageLabel">Write or paste the message you received from your loved one:</label>
            <textarea id="receivedMessage" placeholder="Paste their sweet message here..."></textarea>
        </div>
        
        <div class="settings">
            <div>
                <label id="styleLabel">Reply Style:</label>
                <select id="replyStyle">
                    <option value="romantic">Romantic</option>
                    <option value="playful">Playful</option>
                    <option value="poetic">Poetic</option>
                    <option value="flirty">Flirty</option>
                </select>
            </div>
            <div>
                <label id="lengthLabel">Length:</label>
                <select id="messageLength">
                    <option value="short">Short</option>
                    <option value="medium" selected>Medium</option>
                    <option value="long">Long</option>
                </select>
            </div>
        </div>
        
        <div class="btn-group">
            <button id="generateBtn">
                <span id="generateText">Generate Love Reply</span>
            </button>
            <button id="copyBtn" class="hidden secondary">
                <span id="copyText">Copy to Clipboard</span>
            </button>
        </div>
        
        <div id="responseBox" class="response-box hidden">
            <p id="responseText">Your generated love reply will appear here...</p>
        </div>
        
        <div class="footer">
            <p id="footerText">Made with ❤️ for lovers everywhere</p>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const generateBtn = document.getElementById('generateBtn');
            const copyBtn = document.getElementById('copyBtn');
            const receivedMessage = document.getElementById('receivedMessage');
            const responseBox = document.getElementById('responseBox');
            const responseText = document.getElementById('responseText');
            const replyStyle = document.getElementById('replyStyle');
            const messageLength = document.getElementById('messageLength');
            const heartBtn = document.getElementById('heartBtn');
            const floatingHearts = document.getElementById('floatingHearts');
            const langButtons = document.querySelectorAll('.lang-btn');
            
            // Current language
            let currentLang = 'en';
            
            // Translations
            const translations = {
                en: {
                    title: "Love Message Autoreply",
                    messageLabel: "Write or paste the message you received from your loved one:",
                    styleLabel: "Reply Style:",
                    lengthLabel: "Length:",
                    generateText: "Generate Love Reply",
                    copyText: "Copy to Clipboard",
                    footerText: "Made with ❤️ for lovers everywhere",
                    placeholder: "Paste their sweet message here...",
                    loading: "Creating the perfect reply for your loved one...",
                    romantic: "Romantic",
                    playful: "Playful",
                    poetic: "Poetic",
                    flirty: "Flirty",
                    short: "Short",
                    medium: "Medium",
                    long: "Long",
                    emptyMessage: "Please enter a message to respond to!",
                    responsePlaceholder: "Your generated love reply will appear here..."
                },
                hi: {
                    title: "प्यार भरा जवाब",
                    messageLabel: "अपने प्रियजन से प्राप्त संदेश लिखें या पेस्ट करें:",
                    styleLabel: "जवाब का प्रकार:",
                    lengthLabel: "लंबाई:",
                    generateText: "प्यार भरा जवाब बनाएं",
                    copyText: "क्लिपबोर्ड पर कॉपी करें",
                    footerText: "प्यार करने वालों के लिए ❤️ से बनाया गया",
                    placeholder: "उनका प्यार भरा संदेश यहाँ पेस्ट करें...",
                    loading: "आपके प्रियजन के लिए सही जवाब तैयार किया जा रहा है...",
                    romantic: "रोमांटिक",
                    playful: "चंचल",
                    poetic: "काव्यात्मक",
                    flirty: "फ्लर्टी",
                    short: "छोटा",
                    medium: "मध्यम",
                    long: "लंबा",
                    emptyMessage: "कृपया जवाब देने के लिए एक संदेश दर्ज करें!",
                    responsePlaceholder: "आपका जनरेट किया गया प्यार भरा जवाब यहां दिखाई देगा..."
                },
                kn: {
                    title: "ಪ್ರೀತಿಯ ಸಂದೇಶ ಸ್ವಯಂ-ಉತ್ತರ",
                    messageLabel: "ನಿಮ್ಮ ಪ್ರೀತಿಪಾತ್ರರಿಂದ ಪಡೆದ ಸಂದೇಶವನ್ನು ಬರೆಯಿರಿ ಅಥವಾ ಅಂಟಿಸಿ:",
                    styleLabel: "ಉತ್ತರ ಶೈಲಿ:",
                    lengthLabel: "ಉದ್ದ:",
                    generateText: "ಪ್ರೀತಿಯ ಉತ್ತರ ರಚಿಸಿ",
                    copyText: "ಕ್ಲಿಪ್ಬೋರ್ಡ್ಗೆ ನಕಲಿಸಿ",
                    footerText: "ಪ್ರೇಮಿಗಳಿಗಾಗಿ ❤️ ನೊಂದಿಗೆ ಮಾಡಲಾಗಿದೆ",
                    placeholder: "ಅವರ ಸಿಹಿ ಸಂದೇಶವನ್ನು ಇಲ್ಲಿ ಅಂಟಿಸಿ...",
                    loading: "ನಿಮ್ಮ ಪ್ರೀತಿಪಾತ್ರರಿಗಾಗಿ ಪರಿಪೂರ್ಣ ಉತ್ತರವನ್ನು ರಚಿಸಲಾಗುತ್ತಿದೆ...",
                    romantic: "ರೊಮ್ಯಾಂಟಿಕ್",
                    playful: "ತಮಾಷೆಯ",
                    poetic: "ಕಾವ್ಯಾತ್ಮಕ",
                    flirty: "ಫ್ಲರ್ಟಿ",
                    short: "ಸಣ್ಣ",
                    medium: "ಮಧ್ಯಮ",
                    long: "ದೀರ್ಘ",
                    emptyMessage: "ಉತ್ತರಿಸಲು ದಯವಿಟ್ಟು ಸಂದೇಶವನ್ನು ನಮೂದಿಸಿ!",
                    responsePlaceholder: "ನಿಮ್ಮ ರಚಿಸಿದ ಪ್ರೀತಿಯ ಉತ್ತರವು ಇಲ್ಲಿ ಕಾಣಿಸುತ್ತದೆ..."
                },
                te: {
                    title: "ప్రేమ సందేశం ఆటో రిప్లాయ్",
                    messageLabel: "మీ ప్రియతముని నుండి అందుకున్న సందేశాన్ని వ్రాయండి లేదా పేస్ట్ చేయండి:",
                    styleLabel: "రిప్లాయ్ శైలి:",
                    lengthLabel: "పొడవు:",
                    generateText: "ప్రేమ సందేశ రిప్లాయ్ రూపొందించండి",
                    copyText: "క్లిప్బోర్డ్కు కాపీ చేయండి",
                    footerText: "ప్రేమికుల కోసం ❤️ తో తయారు చేయబడింది",
                    placeholder: "వారి తీయని సందేశాన్ని ఇక్కడ పేస్ట్ చేయండి...",
                    loading: "మీ ప్రియతముని కోసం సరైన రిప్లాయ్ తయారు చేయబడుతోంది...",
                    romantic: "రొమాంటిక్",
                    playful: "సరదా",
                    poetic: "కవిత్వం",
                    flirty: "ఫ్లర్టీ",
                    short: "చిన్నది",
                    medium: "మధ్యస్థం",
                    long: "పొడవైన",
                    emptyMessage: "స్పందించడానికి దయచేసి ఒక సందేశాన్ని నమోదు చేయండి!",
                    responsePlaceholder: "మీ రూపొందించిన ప్రేమ సందేశం ఇక్కడ కనిపిస్తుంది..."
                }
            };
            
            // Love message database for all languages
            const messagesDB = {
                en: {
                    romantic: [
                        "My heart skips a beat every time I think of you.",
                        "Your love is the light that brightens my darkest days.",
                        "I fall in love with you more each passing moment.",
                        "You are my today and all of my tomorrows.",
                        "In your arms is where I belong, now and forever."
                    ],
                    playful: [
                        "If you were a vegetable, you'd be a cute-cumber!",
                        "Are you a magician? Because whenever I look at you, everyone else disappears!",
                        "Do you have a map? I keep getting lost in your eyes.",
                        "Is your name Google? Because you have everything I've been searching for.",
                        "If kisses were snowflakes, I'd send you a blizzard!"
                    ],
                    poetic: [
                        "Like the moon needs the stars, like the shore needs the sea, I need you beside me.",
                        "Your love is the poetry my heart longs to write.",
                        "In the garden of my heart, you are the most beautiful bloom.",
                        "Our love is a melody that plays in perfect harmony.",
                        "You are the missing verse to my incomplete poem."
                    ],
                    flirty: [
                        "I must be a snowflake, because I've fallen for you.",
                        "Are you made of copper and tellurium? Because you're Cu-Te.",
                        "If I could rearrange the alphabet, I'd put U and I together.",
                        "Do you believe in love at first sight, or should I walk by again?",
                        "Is your dad a boxer? Because you're a knockout!"
                    ]
                },
                hi: {
                    romantic: [
                        "तुम्हारे बारे में सोचते ही मेरा दिल धड़कने लगता है।",
                        "तुम्हारा प्यार वह प्रकाश है जो मेरे सबसे अंधेरे दिनों को रोशन करता है।",
                        "हर पल मैं तुम्हें और अधिक प्यार करने लगता हूँ।",
                        "तुम मेरा आज और मेरे सभी कल हो।",
                        "तुम्हारी बाहों में ही मेरा स्थान है, अब और हमेशा के लिए।"
                    ],
                    playful: [
                        "अगर तुम सब्जी होती, तो तुम एक क्यूट-कुम्बर होती!",
                        "क्या तुम जादूगर हो? क्योंकि जब भी मैं तुम्हें देखता हूँ, बाकी सब गायब हो जाते हैं!",
                        "क्या तुम्हारे पास नक्शा है? मैं तुम्हारी आँखों में खो जाता हूँ।",
                        "क्या तुम्हारा नाम गूगल है? क्योंकि तुममें वह सब कुछ है जिसकी मुझे तलाश थी।",
                        "अगर चुंबन बर्फ के टुकड़े होते, तो मैं तुम्हें बर्फ़ीला तूफ़ान भेजता!"
                    ],
                    poetic: [
                        "जैसे चाँद को तारों की ज़रूरत होती है, जैसे किनारे को समुद्र की, मुझे तुम्हारी ज़रूरत है मेरे पास।",
                        "तुम्हारा प्यार वह कविता है जिसे मेरा दिल लिखना चाहता है।",
                        "मेरे दिल के बगीचे में, तुम सबसे सुंदर फूल हो।",
                        "हमारा प्यार एक मधुर संगीत है जो सही सुर में बजता है।",
                        "तुम मेरी अधूरी कविता का वह छंद हो जो गायब था।"
                    ],
                    flirty: [
                        "मैं शायद बर्फ़ का टुकड़ा हूँ, क्योंकि मैं तुम पर गिर गया हूँ।",
                        "क्या तुम तांबे और टेल्यूरियम से बनी हो? क्योंकि तुम Cu-Te हो।",
                        "अगर मैं वर्णमाला को फिर से व्यवस्थित कर सकता, तो मैं U और I को साथ रखता।",
                        "क्या तुम पहली नज़र के प्यार में विश्वास करती हो, या मुझे फिर से चलकर आना चाहिए?",
                        "क्या तुम्हारे पिता बॉक्सर हैं? क्योंकि तुम एक नॉकआउट हो!"
                    ]
                },
                kn: {
                    romantic: [
                        "ನಾನು ನಿನ್ನ ಬಗ್ಗೆ ಯೋಚಿಸಿದಾಗಲೆಲ್ಲಾ ನನ್ನ ಹೃದಯ ಬಡಿತವನ್ನು ತಪ್ಪಿಸುತ್ತದೆ.",
                        "ನಿಮ್ಮ ಪ್ರೀತಿಯು ನನ್ನ ಕತ್ತಲೆಯ ದಿನಗಳನ್ನು ಪ್ರಕಾಶಮಾನಗೊಳಿಸುವ ಬೆಳಕು.",
                        "ಪ್ರತಿ ಕ್ಷಣವೂ ನಾನು ನಿಮ್ಮನ್ನು ಇನ್ನಷ್ಟು ಪ್ರೀತಿಸುತ್ತೇನೆ.",
                        "ನೀವು ನನ್ನ ಇಂದು ಮತ್ತು ನನ್ನ ಎಲ್ಲಾ ನಾಳೆಗಳು.",
                        "ನಿಮ್ಮ ತೋಳುಗಳಲ್ಲಿ ನಾನು ಸೇರಿದ್ದೇನೆ, ಈಗ ಮತ್ತು ಶಾಶ್ವತವಾಗಿ."
                    ],
                    playful: [
                        "ನೀವು ತರಕಾರಿಯಾಗಿದ್ದರೆ, ನೀವು ಒಂದು ಕ್ಯೂಟ್-ಕುಂಬರ್ ಆಗಿರುತ್ತೀರಿ!",
                        "ನೀವು ಮಾಟಗಾರರೇ? ಯಾಕೆಂದರೆ ನಾನು ನಿಮ್ಮನ್ನು ನೋಡಿದಾಗ, ಎಲ್ಲರೂ ಅದೃಶ್ಯರಾಗುತ್ತಾರೆ!",
                        "ನಿಮ್ಮ ಬಳಿ ನಕ್ಷೆ ಇದೆಯೇ? ನಾನು ನಿಮ್ಮ ಕಣ್ಣುಗಳಲ್ಲಿ ಕಳೆದುಹೋಗುತ್ತಿದ್ದೇನೆ.",
                        "ನಿಮ್ಮ ಹೆಸರು ಗೂಗಲ್ ಆಗಿದೆಯೇ? ಯಾಕೆಂದರೆ ನೀವು ನಾನು ಹುಡುಕುತ್ತಿರುವ ಎಲ್ಲವನ್ನೂ ಹೊಂದಿದ್ದೀರಿ.",
                        "ಚುಂಬನಗಳು ಹಿಮದ ಹರಳುಗಳಾಗಿದ್ದರೆ, ನಾನು ನಿಮಗೆ ಹಿಮಪಾತವನ್ನು ಕಳುಹಿಸುತ್ತಿದ್ದೆನು!"
                    ],
                    poetic: [
                        "ಚಂದ್ರನಿಗೆ ನಕ್ಷತ್ರಗಳ ಅಗತ್ಯವಿರುವಂತೆ, ಕರಾವಳಿಗೆ ಸಮುದ್ರದ ಅಗತ್ಯವಿರುವಂತೆ, ನನಗೆ ನೀವು ನನ್ನ ಪಕ್ಕದಲ್ಲಿ ಬೇಕು.",
                        "ನಿಮ್ಮ ಪ್ರೀತಿಯು ನನ್ನ ಹೃದಯವು ಬರೆಯಲು ಬಯಸುವ ಕವಿತೆಯಾಗಿದೆ.",
                        "ನನ್ನ ಹೃದಯದ ತೋಟದಲ್ಲಿ, ನೀವು ಅತ್ಯಂತ ಸುಂದರವಾದ ಹೂವು.",
                        "ನಮ್ಮ ಪ್ರೀತಿಯು ಸಂಪೂರ್ಣ ಸಾಮರಸ್ಯದಲ್ಲಿ ನುಡಿಸುವ ಸಂಗೀತವಾಗಿದೆ.",
                        "ನೀವು ನನ್ನ ಅಪೂರ್ಣ ಕವಿತೆಯ ಕಾಣೆಯಾದ ಪದ್ಯವಾಗಿದ್ದೀರಿ."
                    ],
                    flirty: [
                        "ನಾನು ಹಿಮದ ಹರಳಾಗಿರಬೇಕು, ಯಾಕೆಂದರೆ ನಾನು ನಿಮ್ಮ ಮೇಲೆ ಬಿದ್ದಿದ್ದೇನೆ.",
                        "ನೀವು ತಾಮ್ರ ಮತ್ತು ಟೆಲ್ಯೂರಿಯಂನಿಂದ ಮಾಡಲ್ಪಟ್ಟಿದ್ದೀರಾ? ಯಾಕೆಂದರೆ ನೀವು Cu-Te ಆಗಿದ್ದೀರಿ.",
                        "ನಾನು ವರ್ಣಮಾಲೆಯನ್ನು ಮತ್ತೆ ಜೋಡಿಸಲು ಸಾಧ್ಯವಾದರೆ, ನಾನು U ಮತ್ತು I ಅನ್ನು ಒಟ್ಟಿಗೆ ಇಡುತ್ತಿದ್ದೆನು.",
                        "ನೀವು ಮೊದಲ ನೋಟದ ಪ್ರೀತಿಯಲ್ಲಿ ನಂಬಿಕೆಯನ್ನು ಹೊಂದಿದ್ದೀರಾ, ಅಥವಾ ನಾನು ಮತ್ತೆ ಹಾದು ಹೋಗಬೇಕು?",
                        "ನಿಮ್ಮ ತಂದೆ ಬಾಕ್ಸರ್ ಆಗಿದ್ದಾರೆಯೇ? ಯಾಕೆಂದರೆ ನೀವು ನಾಕ್ಔಟ್ ಆಗಿದ್ದೀರಿ!"
                    ]
                },
                te: {
                    romantic: [
                        "నేను నిన్ను గురించి ఆలోచించిన ప్రతిసారీ నా హృదయం ఒక బీట్ మిస్ అవుతుంది.",
                        "మీ ప్రేమ నా చీకటి రోజులను ప్రకాశవంతం చేసే కాంతి.",
                        "ప్రతి క్షణం గడిచే కొద్దీ నేను మీతో ప్రేమలో పడుతున్నాను.",
                        "మీరు నా ఈరోజు మరియు నా అన్ని రేపులు.",
                        "మీ బాహువుల్లోనే నాకు చెందినది, ఇప్పుడు మరియు ఎప్పటికీ."
                    ],
                    playful: [
                        "మీరు ఒక కూరగాయ అయితే, మీరు ఒక క్యూట్-కుకుంబర్ అవుతారు!",
                        "మీరు మాంత్రికుడా? ఎందుకంటే నేను మిమ్మల్ని చూసినప్పుడు, మిగతావారంతా అదృశ్యమవుతారు!",
                        "మీ దగ్గర మ్యాప్ ఉందా? నేను మీ కళ్ళలో కోల్పోతున్నాను.",
                        "మీ పేరు గూగుల్ అనా? ఎందుకంటే మీరు నేను వెతుకుతున్న ప్రతిదీ కలిగి ఉన్నారు.",
                        "ముద్దులు హిమపాతం అయితే, నేను మీకు ఒక హిమపాతం పంపుతాను!"
                    ],
                    poetic: [
                        "చంద్రునికి నక్షత్రాలు అవసరమైనట్లు, తీరానికి సముద్రం అవసరమైనట్లు, నాకు మీరు నా పక్కన అవసరం.",
                        "మీ ప్రేమ నా హృదయం రాయాలనుకునే కవిత.",
                        "నా హృదయం తోటలో, మీరు అత్యంత అందమైన పువ్వు.",
                        "మన ప్రేమ పరిపూర్ణ సామరస్యంతో వాయించే సంగీతం.",
                        "మీరు నా అసంపూర్ణ కవిత యొక్క తప్పిపోయిన పద్యం."
                    ],
                    flirty: [
                        "నేను ఒక హిమపాతం కావాలి, ఎందుకంటే నేను మీ కోసం పడిపోయాను.",
                        "మీరు రాగి మరియు టెల్లూరియంతో తయారు చేయబడ్డారా? ఎందుకంటే మీరు Cu-Te.",
                        "నేను వర్ణమాలను మళ్లీ అమర్చగలిగితే, నేను U మరియు I ని కలిపి ఉంచేవాడిని.",
                        "మీరు మొదటి చూపులో ప్రేమను నమ్ముతారా, లేక నేను మళ్లీ నడవాలా?",
                        "మీ తండ్రి బాక్సర్ అనా? ఎందుకంటే మీరు నాక్ఔట్!"
                    ]
                }
            };
            
            // Create floating hearts
            function createFloatingHearts() {
                for (let i = 0; i < 15; i++) {
                    const heart = document.createElement('div');
                    heart.className = 'floating-heart';
                    heart.innerHTML = '❤️';
                    heart.style.left = Math.random() * 100 + 'vw';
                    heart.style.animationDuration = 5 + Math.random() * 10 + 's';
                    heart.style.animationDelay = Math.random() * 5 + 's';
                    floatingHearts.appendChild(heart);
                }
            }
            
            // Change language
            function changeLanguage(lang) {
                currentLang = lang;
                const t = translations[lang];
                
                // Update UI text
                document.getElementById('appTitle').textContent = t.title;
                document.getElementById('messageLabel').textContent = t.messageLabel;
                document.getElementById('styleLabel').textContent = t.styleLabel;
                document.getElementById('lengthLabel').textContent = t.lengthLabel;
                document.getElementById('generateText').textContent = t.generateText;
                document.getElementById('copyText').textContent = t.copyText;
                document.getElementById('footerText').textContent = t.footerText;
                document.getElementById('receivedMessage').placeholder = t.placeholder;
                document.getElementById('responseText').textContent = t.responsePlaceholder;
                
                // Update dropdown options
                const styleSelect = document.getElementById('replyStyle');
                styleSelect.innerHTML = `
                    <option value="romantic">${t.romantic}</option>
                    <option value="playful">${t.playful}</option>
                    <option value="poetic">${t.poetic}</option>
                    <option value="flirty">${t.flirty}</option>
                `;
                
                const lengthSelect = document.getElementById('messageLength');
                lengthSelect.innerHTML = `
                    <option value="short">${t.short}</option>
                    <option value="medium" selected>${t.medium}</option>
                    <option value="long">${t.long}</option>
                `;
            }
            
            // Language selector event
            langButtons.forEach(btn => {
                btn.addEventListener('click', function() {
                    langButtons.forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    changeLanguage(this.dataset.lang);
                });
            });
            
            // Generate love message
            generateBtn.addEventListener('click', function() {
                if (receivedMessage.value.trim() === '') {
                    alert(translations[currentLang].emptyMessage);
                    return;
                }
                
                responseBox.classList.remove('hidden');
                responseText.innerHTML = `<span class="loading">${translations[currentLang].loading}</span>`;
                copyBtn.classList.add('hidden');
                
                // Simulate processing delay
                setTimeout(() => {
                    const style = replyStyle.value;
                    const length = messageLength.value;
                    
                    let messages = messagesDB[currentLang][style];
                    let selectedMessages = [];
                    
                    // Shuffle array
                    messages = messages.sort(() => 0.5 - Math.random());
                    
                    // Select based on length
                    let count = 1;
                    if (length === 'medium') count = 2;
                    if (length === 'long') count = 3;
                    
                    selectedMessages = messages.slice(0, count + 1);
                    
                    // Add personalization based on received message
                    const receivedText = receivedMessage.value.toLowerCase();
                    let personalized = '';
                    
                    if (receivedText.includes('miss you') || receivedText.includes('missing you')) {
                        personalized = currentLang === 'en' ? "I miss you more than words can say. " :
                                      currentLang === 'hi' ? "मैं तुम्हें शब्दों से कहीं अधिक याद करता हूँ। " :
                                      currentLang === 'kn' ? "ನಾನು ನಿಮ್ಮನ್ನು ಹೇಳಲಾಗದಷ್ಟು ಮಿಸ್ ಮಾಡುತ್ತೇನೆ. " :
                                      "నేను మిమ్మల్ని మాటలతో చెప్పలేనంతగా మిస్ అవుతున్నాను. ";
                    } else if (receivedText.includes('love you') || receivedText.includes('loving you')) {
                        personalized = currentLang === 'en' ? "I love you more than you'll ever know. " :
                                      currentLang === 'hi' ? "मैं तुम्हें तुम्हारी सोच से भी अधिक प्यार करता हूँ। " :
                                      currentLang === 'kn' ? "ನಾನು ನಿಮಗೆ ತಿಳಿಯದಷ್ಟು ಪ್ರೀತಿಸುತ್ತೇನೆ. " :
                                      "నేను మీకు తెలియనంతగా ప్రేమిస్తున్నాను. ";
                    } else if (receivedText.includes('thinking of you') || receivedText.includes('think of you')) {
                        personalized = currentLang === 'en' ? "You're always in my thoughts. " :
                                      currentLang === 'hi' ? "तुम हमेशा मेरे विचारों में हो। " :
                                      currentLang === 'kn' ? "ನೀವು ಯಾವಾಗಲೂ ನನ್ನ ಆಲೋಚನೆಗಳಲ್ಲಿರುತ್ತೀರಿ. " :
                                      "మీరు ఎల్లప్పుడూ నా ఆలోచనల్లో ఉంటారు. ";
                    } else if (receivedText.includes('beautiful') || receivedText.includes('handsome')) {
                        personalized = currentLang === 'en' ? "You're the beautiful/handsome one! " :
                                      currentLang === 'hi' ? "तुम ही सुंदर/हैंडसम हो! " :
                                      currentLang === 'kn' ? "ನೀವು ಸುಂದರ/ಹ್ಯಾಂಡ್ಸಮ್! " :
                                      "మీరు అందమైన/హ్యాండ్సమ్! ";
                    }
                    
                    // Construct response
                    let response = personalized + selectedMessages.join(' ');
                    
                    // Add closing
                    const closings = {
                        en: [
                            " Can't wait to see you soon!",
                            " Sending you all my love.",
                            " Counting the moments until we're together again.",
                            " You mean the world to me."
                        ],
                        hi: [
                            " जल्द ही तुम्हें देखने का इंतज़ार नहीं कर सकता!",
                            " तुम्हें मेरा सारा प्यार भेज रहा हूँ।",
                            " हमारे फिर से साथ होने के पलों की गिनती कर रहा हूँ।",
                            " तुम मेरी दुनिया हो।"
                        ],
                        kn: [
                            " ನಿಮ್ಮನ್ನು ಶೀಘ್ರದಲ್ಲೇ ನೋಡಲು ಕಾಯಲು ಸಾಧ್ಯವಿಲ್ಲ!",
                            " ನಿಮಗೆ ನನ್ನ ಎಲ್ಲಾ ಪ್ರೀತಿಯನ್ನು ಕಳುಹಿಸುತ್ತಿದ್ದೇನೆ.",
                            " ನಾವು ಮತ್ತೆ ಒಟ್ಟಿಗೆ ಸಿಗುವ ತನಕ ಕ್ಷಣಗಳನ್ನು ಎಣಿಸುತ್ತಿದ್ದೇನೆ.",
                            " ನೀವು ನನಗೆ ಪ್ರಪಂಚ."
                        ],
                        te: [
                            " త్వరలో మిమ్మల్ని చూడటానికి వేచి ఉండలేను!",
                            " మీకు నా ప్రేమనంతా పంపుతున్నాను.",
                            " మేము మళ్లీ కలిసే వరకు క్షణాలను లెక్కిస్తున్నాను.",
                            " మీరు నాకు ప్రపంచం."
                        ]
                    };
                    
                    response += closings[currentLang][Math.floor(Math.random() * closings[currentLang].length)];
                    
                    // Display response
                    responseText.textContent = response;
                    copyBtn.classList.remove('hidden');
                }, 1500);
            });
            
            // Copy to clipboard
            copyBtn.addEventListener('click', function() {
                navigator.clipboard.writeText(responseText.textContent)
                    .then(() => {
                        const originalText = copyBtn.querySelector('span').textContent;
                        copyBtn.querySelector('span').textContent = translations[currentLang].copyText === 'Copy to Clipboard' ? 'Copied!' :
                                                                     translations[currentLang].copyText === 'क्लिपबोर्ड पर कॉपी करें' ? 'कॉपी किया गया!' :
                                                                     translations[currentLang].copyText === 'ಕ್ಲಿಪ್ಬೋರ್ಡ್ಗೆ ನಕಲಿಸಿ' ? 'ನಕಲಿಸಲಾಗಿದೆ!' :
                                                                     'కాపీ చేయబడింది!';
                        setTimeout(() => {
                            copyBtn.querySelector('span').textContent = originalText;
                        }, 2000);
                    })
                    .catch(err => {
                        console.error('Failed to copy: ', err);
                    });
            });
            
            // Heart button animation
            heartBtn.addEventListener('click', function() {
                this.style.transform = 'scale(1.5)';
                setTimeout(() => {
                    this.style.transform = 'scale(1)';
                }, 300);
                
                // Create a temporary floating heart
                const tempHeart = document.createElement('div');
                tempHeart.className = 'floating-heart';
                tempHeart.innerHTML = '❤️';
                tempHeart.style.left = '50%';
                tempHeart.style.top = '50%';
                tempHeart.style.position = 'fixed';
                tempHeart.style.animation = 'float 3s linear forwards';
                tempHeart.style.opacity = '0.8';
                document.body.appendChild(tempHeart);
                
                setTimeout(() => {
                    tempHeart.remove();
                }, 3000);
            });
            
            // Initialize
            createFloatingHearts();
        });
    </script>
</body>
</html>
