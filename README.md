<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Smart Chatbot</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #e5ddd5;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .chat-container {
            width: 100%;
            max-width: 450px;
            height: 80vh;
            background: #fff;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        .chat-header {
            background-color: #075e54;
            color: white;
            padding: 15px 20px;
            font-size: 18px;
            font-weight: 600;
            display: flex;
            align-items: center;
        }
        .chat-header span {
            display: inline-block;
            width: 10px;
            height: 10px;
            background-color: #25d366;
            border-radius: 50%;
            margin-right: 10px;
        }
        .chat-box {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            background-color: #ece5dd;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        .message {
            max-width: 80%;
            padding: 10px 15px;
            border-radius: 15px;
            font-size: 14px;
            line-height: 1.4;
            word-wrap: break-word;
        }
        .user-msg {
            background-color: #dcf8c6;
            align-self: flex-end;
            border-bottom-right-radius: 0;
        }
        .bot-msg {
            background-color: #fff;
            align-self: flex-start;
            border-bottom-left-radius: 0;
            box-shadow: 0 1px 2px rgba(0,0,0,0.1);
        }
        .input-area {
            display: flex;
            padding: 15px;
            background: #f0f0f0;
            border-top: 1px solid #ddd;
        }
        input[type="text"] {
            flex: 1;
            padding: 12px 15px;
            border: none;
            border-radius: 20px;
            outline: none;
            font-size: 14px;
        }
        button {
            background-color: #128c7e;
            color: white;
            border: none;
            padding: 10px 20px;
            margin-left: 10px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
        }
        button:hover {
            background-color: #075e54;
        }
        .typing {
            font-size: 12px;
            color: #888;
            font-style: italic;
            display: none;
        }
    </style>
</head>
<body>

<div class="chat-container">
    <div class="chat-header">
        <span></span> AI Assistant
    </div>
    
    <div class="chat-box" id="chatBox">
        <div class="message bot-msg">Hello! Main ek AI chatbot hoon. Aap mujhse koi bhi sawal pooch sakte hain.</div>
    </div>
    
    <div class="input-area">
        <input type="text" id="userInput" placeholder="Type your question here..." onkeypress="handleEnter(event)">
        <button onclick="sendMessage()">Send</button>
    </div>
</div>

<script>
    // ⚠️ YAHAN APNI GOOGLE GEMINI API KEY DALEIN
    const API_KEY = "YOUR_API_KEY_HERE"; 

    const chatBox = document.getElementById('chatBox');
    const userInput = document.getElementById('userInput');

    function handleEnter(event) {
        if (event.key === "Enter") sendMessage();
    }

    async function sendMessage() {
        const text = userInput.value.trim();
        if (!text) return;

        // User ka message UI mein add karein
        appendMessage(text, 'user-msg');
        userInput.value = '';

        // Typing indicator dikhayein
        const typingId = appendMessage('Typing...', 'bot-msg typing');

        try {
            // API Call setup
            const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=${API_KEY}`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    contents: [{ parts: [{ text: text }] }]
                })
            });

            const data = await response.json();
            
            // Remove typing indicator
            document.getElementById(typingId).remove();

            // API se jo text aaya usko extract karein
            if (data.candidates && data.candidates[0].content.parts[0].text) {
                const botReply = data.candidates[0].content.parts[0].text;
                appendMessage(botReply, 'bot-msg');
            } else {
                appendMessage("Sorry, mujhe samajh nahi aaya. Please try again.", 'bot-msg');
            }

        } catch (error) {
            console.error(error);
            document.getElementById(typingId).remove();
            appendMessage("Error: API Key check karein ya internet connection verify karein.", 'bot-msg');
        }
    }

    function appendMessage(text, className) {
        const msgDiv = document.createElement('div');
        msgDiv.className = `message ${className}`;
        
        // ID set karna zaruri hai typing indicator remove karne ke liye
        const id = 'msg-' + Date.now();
        msgDiv.id = id;
        
        // Simple text formatting for basic line breaks
        msgDiv.innerHTML = text.replace(/\n/g, '<br>');
        
        chatBox.appendChild(msgDiv);
        chatBox.scrollTop = chatBox.scrollHeight; // Auto-scroll to bottom
        
        return id;
    }
</script>

</body>
</html>
