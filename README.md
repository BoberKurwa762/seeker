<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Seeker</title>
    <style>
        body {
            background: linear-gradient(to bottom, rgb(15, 15, 15), rgb(10, 10, 10));
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            font-family: Arial, sans-serif;
            color: white;
            opacity: 0;
            animation: fadeInBody 1s ease-out forwards;
        }

        @keyframes fadeInBody {
            to { opacity: 1; }
        }

        .welcome-text {
            color: white;
            font-size: 2.5em;
            margin-top: 30px;
            padding: 20px 40px;
            display: inline-block;
            white-space: nowrap;
            overflow: hidden;
            font-weight: bold;
            text-align: center;
            opacity: 1;
            transform: translateY(20px);
            animation: fadeInText 1s ease-out 0.5s forwards;
            text-shadow: 0 0 5px rgba(255, 255, 255, 0.7),
                        0 0 10px rgba(255, 255, 255, 0.5),
                        0 0 15px rgba(255, 255, 255, 0.3);
            animation: textGlow 3s ease-in-out infinite alternate;
        }

        @keyframes fadeInText {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes textGlow {
            from {
                text-shadow: 0 0 5px rgba(255, 255, 255, 0.5),
                            0 0 10px rgba(255, 255, 255, 0.3),
                            0 0 15px rgba(255, 255, 255, 0.1);
            }
            to {
                text-shadow: 0 0 10px rgba(255, 255, 255, 0.8),
                            0 0 20px rgba(255, 255, 255, 0.6),
                            0 0 30px rgba(255, 255, 255, 0.4);
            }
        }

        .tabs {
            display: flex;
            gap: 20px;
            margin: 20px 0;
            opacity: 1;
            animation: fadeInText 1s ease-out 0.8s forwards;
        }

        .tab-btn {
            background-color: #1e90ff;
            color: white !important;
            padding: 10px 20px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            font-size: 1.1em;
            cursor: pointer;
            position: relative;
            transition: box-shadow 0.3s ease-in-out, background-color 0.3s ease-in-out;
            box-shadow: none;
        }

        .tab-btn:hover {
            background-color: #1e90ff;
            box-shadow: 0 0 15px rgba(0, 191, 255, 0.8),
                       0 0 30px rgba(0, 191, 255, 0.6),
                       0 0 45px rgba(0, 191, 255, 0.4),
                       inset 0 0 20px rgba(0, 191, 255, 0.5);
            color: white !important;
        }

        .tab-btn.active {
            background-color: #1e90ff;
            color: white !important;
            box-shadow: 0 0 10px rgba(0, 191, 255, 0.6);
        }

        .tab-btn.credits-btn {
            background-color: #ff3333; /* Red color */
        }

        .tab-btn.credits-btn:hover {
            background-color: #ff3333;
            box-shadow: 0 0 15px rgba(255, 51, 51, 0.8),
                       0 0 30px rgba(255, 51, 51, 0.6),
                       0 0 45px rgba(255, 51, 51, 0.4),
                       inset 0 0 20px rgba(255, 51, 51, 0.5);
        }

        .tab-btn.credits-btn.active {
            background-color: #ff3333;
            box-shadow: 0 0 10px rgba(255, 51, 51, 0.6);
        }

        .tab-content {
            display: none;
            width: 100%;
            max-width: 600px;
            opacity: 0;
            transition: opacity 0.6s ease-in-out;
        }

        .tab-content.active {
            display: block;
            opacity: 1;
        }

        .info-section {
            background-color: #1a1a1a;
            border: 1px solid #333;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            width: 100%;
            max-width: 400px;
            position: relative;
            overflow: hidden;
            opacity: 1;
            transform: translateY(20px);
            animation: fadeInSection 1s ease-out forwards;
            box-shadow: 0 0 5px rgba(255, 255, 255, 0.1);
            transition: box-shadow 0.6s ease-in-out;
        }

        .info-section:hover {
            box-shadow: 0 0 15px rgba(27, 27, 26, 0.7), 
                       0 0 30px rgba(27, 27, 26, 0.5), 
                       0 0 45px rgba(27, 27, 26, 0.3);
        }

        @keyframes fadeInSection {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .info-section h2 {
            font-size: 1.5em;
            margin: 0 0 15px;
            color: white;
            display: inline-block;
        }

        .info-section ul {
            list-style-type: none;
            padding: 0;
            margin: 0 0 20px;
        }

        .info-section li {
            color: #ccc;
            font-size: 1em;
            margin: 10px 0;
            position: relative;
            padding-left: 20px;
        }

        .info-section li:before {
            content: "•";
            color: #666;
            position: absolute;
            left: 0;
        }

        .premium-section {
            background-color: #222;
            padding: 15px;
            margin: 20px 0;
            border-radius: 10px;
            border: 1px solid #444;
            position: relative;
            width: 100%;
            max-width: 800px;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-10px);
            }
            100% {
                transform: translateY(0);
            }
        }

        .premium-section h3 {
            font-size: 1.2em;
            margin: 0 0 10px;
            color: #fff;
            font-weight: bold;
            text-shadow: 0 0 5px rgba(255, 255, 255, 0.6), 
                        0 0 10px rgba(255, 255, 255, 0.4), 
                        0 0 15px rgba(255, 255, 255, 0.2);
        }

        .premium-section ul {
            list-style-type: none;
            padding: 0;
            margin: 0 0 10px;
            color: #ccc;
        }

        .premium-section li {
            margin: 5px 0;
            padding-left: 20px;
            position: relative;
            text-shadow: 0 0 5px rgba(255, 255, 255, 0.6), 
                        0 0 10px rgba(255, 255, 255, 0.4), 
                        0 0 15px rgba(255, 255, 255, 0.2);
        }

        .premium-section li:before {
            content: "•";
            color: #ccc;
            position: absolute;
            left: 0;
            text-shadow: 0 0 5px rgba(255, 255, 255, 0.6), 
                        0 0 10px rgba(255, 255, 255, 0.4), 
                        0 0 15px rgba(255, 255, 255, 0.2);
        }

        .premium-section .price {
            position: absolute;
            top: 15px;
            right: 15px;
            color: #fff;
            font-size: 1.2em;
            font-weight: bold;
            text-shadow: none;
        }

        .premium-section .price-subtext {
            font-size: 0.8em;
            color: #666;
            display: block;
            text-shadow: none;
        }

        .premium-section .purchase-btn {
            background-color: #333;
            border: none;
            color: white;
            padding: 8px 15px;
            border-radius: 5px;
            font-size: 0.9em;
            cursor: pointer;
            width: 100%;
            text-align: center;
            transition: background-color 0.3s ease, color 0.3s ease, box-shadow 0.3s ease;
            box-shadow: none;
        }

        .premium-section .purchase-btn:hover {
            background-color: #555;
            color: #e0e0e0;
            box-shadow: 0 0 15px rgba(128, 128, 128, 0.7),
                       0 0 30px rgba(128, 128, 128, 0.5),
                       0 0 45px rgba(128, 128, 128, 0.3),
                       inset 0 0 20px rgba(128, 128, 128, 0.5);
        }

        .learn-more-btn, .download-api-btn, .buy-premium-btn {
            background-color: transparent;
            border: 1px solid #666;
            color: #ccc;
            padding: 10px 20px;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 5px;
            transition: background-color 0.6s ease-in-out, 
                       color 0.6s ease-in-out, 
                       border-color 0.6s ease-in-out, 
                       box-shadow 0.3s ease-in-out;
            box-shadow: none;
            text-decoration: none;
            box-sizing: border-box;
        }

        .learn-more-btn:hover, .download-api-btn:hover, .buy-premium-btn:hover {
            background-color: #333;
            color: white;
            border-color: white;
            box-shadow: 0 0 15px rgba(5, 5, 5, 0.7),
                       0 0 30px rgba(5, 5, 5, 0.5),
                       0 0 45px rgba(5, 5, 5, 0.3),
                       inset 0 0 20px rgba(5, 5, 5, 0.5);
        }

        .learn-more-btn::before {
            content: "⟐";
            font-size: 1.2em;
        }

        .download-api-btn::before {
            content: "⟐";
            font-size: 1.2em;
        }

        .buy-premium-btn::before {
            content: "⟐";
            font-size: 1.2em;
        }

        .hidden-audio {
            display: none;
        }
    </style>
</head>
<body>
    <div class="welcome-text" id="typewriter"></div>

    <div class="tabs">
        <button class="tab-btn active" onclick="openTab('about')">About</button>
        <button class="tab-btn" onclick="openTab('how-we-created')">Some Stuff</button>
        <button class="tab-btn credits-btn" onclick="openTab('credits')">Credits</button>
    </div>

    <div class="premium-section">
        <h3>Premium Features</h3>
        <span class="price">$3.99<span class="price-subtext">/Month</span></span>
        <ul>
            <li>96% UNC</li>
            <li>90% sUNC</li>
            <li>Level 6</li>
        </ul>
        <button class="purchase-btn">Purchase</button>
    </div>

    <div id="about" class="tab-content active">
        <div class="info-section">
            <h2>Seeker API</h2>
            <ul>
                <li>Fast Injection</li>
                <li>Xeno Based</li>
                <li>Easy Setup</li>
            </ul>
            <a href="https://cdn.discordapp.com/attachments/1320345944188784704/1344752080480501894/CCAPI.zip?ex=67c2b638&is=67c164b8&hm=a3a0507a438cdc3e5b69e385ac1efb734cfc00cef67b2e5bae22d48c28f4ce8a&" target="_blank" class="download-api-btn">Download API</a>
        </div>
        <div class="info-section">
            <h2>Community</h2>
            <ul>
                <li>Active Support</li>
                <li>Regular Updates</li>
                <li>Feedback Driven</li>
            </ul>
            <button class="learn-more-btn">Learn More</button>
        </div>
        <div class="info-section">
            <h2>Free Features</h2>
            <ul>
                <li>80% UNC</li>
                <li>Level 3</li>
                <li>Not Really Secure</li>
                <li>Premium Coming Soon!</li>
            </ul>
            <a href="https://cdn.discordapp.com/attachments/1320345944188784704/1344752080480501894/CCAPI.zip?ex=67c2b638&is=67c164b8&hm=a3a0507a438cdc3e5b69e385ac1efb734cfc00cef67b2e5bae22d48c28f4ce8a&" target="_blank" class="download-api-btn">Check Out!</a>
        </div>
    </div>

    <div id="how-we-created" class="tab-content">
        <div class="info-section">
            <h2>Good things about our discord server</h2>
            <ul>
                <li>Cracked Software</li>
            </ul>
            <a href="https://discord.gg/v5BmWt8tK3" target="_blank" class="learn-more-btn">Learn More</a>
        </div>
    </div>

    <div id="credits" class="tab-content">
        <div class="info-section">
            <h2>Our Team</h2>
            <ul>
                <li>@Skibidi Skidz - Full-Owner/Developer/Founder</li>
                <li>@TheCzech- Co-Owner/Developer</li>
                <li>https://discord.gg/seeker</li>
            </ul>
            <button class="learn-more-btn">Learn More</button>
        </div>
    </div>

    <audio class="hidden-audio" autoplay loop>
        <source src="path/to/serialkilla.mp3" type="audio/mpeg">
    </audio>

    <script>
        function openTab(tabName) {
            const tabContents = document.getElementsByClassName("tab-content");
            for (let i = 0; i < tabContents.length; i++) {
                tabContents[i].classList.remove("active");
            }

            const tabButtons = document.getElementsByClassName("tab-btn");
            for (let i = 0; i < tabButtons.length; i++) {
                tabButtons[i].classList.remove("active");
            }

            document.getElementById(tabName).classList.add("active");
            event.currentTarget.classList.add("active");
        }

        const typewriterElement = document.getElementById("typewriter");
        const phrases = [
            "Powerful cheating tool",
            "Made with love",
            "Get seeker now",
            "Learn more on the about"
        ];

        const capitalizedPhrases = phrases.map(phrase => 
            phrase.charAt(0).toUpperCase() + phrase.slice(1)
        );

        let phraseIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        let typingSpeed = 100;

        function type() {
            const currentPhrase = capitalizedPhrases[phraseIndex];
            if (!isDeleting) {
                typewriterElement.textContent = currentPhrase.substring(0, charIndex);
                charIndex++;
                if (charIndex > currentPhrase.length) {
                    isDeleting = true;
                    setTimeout(type, 1500);
                    return;
                }
            } else {
                typewriterElement.textContent = currentPhrase.substring(0, charIndex);
                charIndex--;
                if (charIndex < 0) {
                    isDeleting = false;
                    phraseIndex = (phraseIndex + 1) % capitalizedPhrases.length;
                    setTimeout(type, 500);
                    return;
                }
            }
            setTimeout(type, isDeleting ? typingSpeed / 2 : typingSpeed);
        }

        type();
    </script>
</body>
</html>
