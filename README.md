<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Discord Server Verification</title>
    <style>
        /* Dark theme styling matching Discord aesthetics */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #2f3136;
            color: #ffffff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .verification-container {
            background-color: #36393f;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
            text-align: center;
            max-width: 400px;
            width: 100%;
        }
        h2 {
            margin-bottom: 10px;
            color: #5865F2; /* Discord Blurple */
        }
        p {
            color: #b9bbbe;
            font-size: 14px;
            line-height: 1.5;
        }
        .input-group {
            margin: 20px 0;
            text-align: left;
        }
        label {
            font-size: 12px;
            color: #b9bbbe;
            text-transform: uppercase;
            font-weight: bold;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            background-color: #202225;
            border: 1px solid #202225;
            border-radius: 4px;
            color: white;
            box-sizing: border-box;
        }
        input[type="text"]:focus {
            border-color: #5865F2;
            outline: none;
        }
        button {
            background-color: #5865F2;
            color: white;
            border: none;
            padding: 12px 20px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 4px;
            cursor: pointer;
            width: 100%;
            transition: background-color 0.2s;
        }
        button:hover {
            background-color: #4752C4;
        }
        .success-msg {
            color: #3ba55d;
            display: none;
            margin-top: 15px;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="verification-container">
    <h2>Server Verification</h2>
    <p>Please enter your exact Discord Username below to complete verification and gain access to the server.</p>
    
    <div class="input-group">
        <label for="username">Discord Username</label>
        <input type="text" id="username" placeholder="e.g., wumpus_coder" required>
    </div>

    <button onclick="sendVerification()">Verify Me</button>
    <div id="successMessage" class="success-msg">✓ Request Sent! Check the server text channels.</div>
</div>

<script>
function sendVerification() {
    const usernameInput = document.getElementById('username').value;
    const successMessage = document.getElementById('successMessage');

    if (!usernameInput) {
        alert("Please enter a valid username.");
        return;
    }

    // PASTE YOUR DISCORD WEBHOOK URL HERE
    const webhookURL = "https://discord.com/api/webhooks/1507725928610926773/D8y_n_mQfghXm6GiAd7-OJrbOOVzjn2VYfCPMUoNas-_tm7KeqpD7zaQQfHKwO6SK4tq";

    // Structuring the data payload payload to look clean on Discord
    const payload = {
        embeds: [{
            title: "🔐 New Verification Request",
            color: 5793266, // Dark Green accent color
            fields: [
                {
                    name: "User Submitted Username",
                    value: `\`${usernameInput}\``,
                    inline: false
                },
                {
                    name: "Status",
                    value: "⏳ Pending manual role assignment or bot processing",
                    inline: false
                }
            ],
            timestamp: new Date().toISOString()
        }]
    };

    // Sending the data directly to Discord using native JS Fetch API
    fetch(webhookURL, {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(payload)
    })
    .then(response => {
        if (response.ok) {
            successMessage.style.display = "block";
            document.getElementById('username').value = ""; // Clear input
        } else {
            alert("Error sending request to Discord. Check your Webhook URL configuration.");
        }
    })
    .catch(error => {
        console.error("Error:", error);
        alert("Something went wrong with the network request.");
    });
}
</script>

</body>
</html>
