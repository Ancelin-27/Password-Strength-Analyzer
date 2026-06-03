<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Password Strength Checker</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>

    <div class="container">

        <h1>Password Strength Checker</h1>

        <div class="input-group">
            <input type="password" id="password" placeholder="Enter Password">
            <button onclick="togglePassword()">Show</button>
        </div>

        <button class="check-btn" onclick="checkPassword()">
            Check Strength
        </button>

        <button class="generate-btn" onclick="generatePassword()">
            Generate Strong Password
        </button>

        <div class="progress-container">
            <div id="progress-bar"></div>
        </div>

        <h2 id="strength"></h2>

        <div id="score"></div>

        <div id="suggestions"></div>

    </div>

    <script src="script.js"></script>

</body>

</html>
 {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #141e30, #243b55);
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.container {
    background: white;
    width: 500px;
    padding: 30px;
    border-radius: 15px;
    text-align: center;
    box-shadow: 0px 0px 20px rgba(0,0,0,0.3);
}

h1 {
    margin-bottom: 20px;
    color: #333;
}

.input-group {
    display: flex;
    gap: 10px;
}

input {
    flex: 1;
    padding: 12px;
    font-size: 16px;
}

button {
    padding: 12px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
}

.check-btn {
    margin-top: 15px;
    width: 100%;
    background: #007bff;
    color: white;
}

.generate-btn {
    margin-top: 10px;
    width: 100%;
    background: #28a745;
    color: white;
}

.progress-container {
    width: 100%;
    height: 25px;
    background: #ddd;
    border-radius: 20px;
    margin-top: 20px;
}

#progress-bar {
    height: 100%;
    width: 0%;
    border-radius: 20px;
    transition: 0.5s;
}

#strength {
    margin-top: 20px;
}

#score {
    margin-top: 10px;
    font-size: 18px;
}

#suggestions {
    margin-top: 15px;
    color: red;
    text-align: left;
}
function checkPassword() {

    let password = document.getElementById("password").value;

    let score = 0;
    let suggestions = [];

    // Length Check
    if (password.length >= 12)
        score += 25;
    else
        suggestions.push("✔ Use at least 12 characters");

    // Uppercase
    if (/[A-Z]/.test(password))
        score += 15;
    else
        suggestions.push("✔ Add uppercase letters");

    // Lowercase
    if (/[a-z]/.test(password))
        score += 15;
    else
        suggestions.push("✔ Add lowercase letters");

    // Number
    if (/[0-9]/.test(password))
        score += 15;
    else
        suggestions.push("✔ Add numbers");

    // Special Character
    if (/[!@#$%^&*(),.?":{}|<>]/.test(password))
        score += 15;
    else
        suggestions.push("✔ Add special characters");

    // Common Password Check
    const commonPasswords = [
        "password",
        "123456",
        "admin",
        "qwerty",
        "welcome",
        "abc123"
    ];

    if (!commonPasswords.includes(password.toLowerCase()))
        score += 15;
    else
        suggestions.push("✔ Avoid common passwords");

    let strength = "";
    let color = "";

    if (score < 40) {
        strength = "Weak";
        color = "red";
    }
    else if (score < 70) {
        strength = "Moderate";
        color = "orange";
    }
    else if (score < 90) {
        strength = "Strong";
        color = "blue";
    }
    else {
        strength = "Very Strong";
        color = "green";
    }

    document.getElementById("strength").innerHTML =
        "Password Strength: " + strength;

    document.getElementById("score").innerHTML =
        "Score: " + score + "/100";

    document.getElementById("progress-bar").style.width =
        score + "%";

    document.getElementById("progress-bar").style.background =
        color;

    if (suggestions.length > 0) {
        document.getElementById("suggestions").innerHTML =
            "<b>Suggestions:</b><br>" +
            suggestions.join("<br>");
    }
    else {
        document.getElementById("suggestions").innerHTML =
            "<span style='color:green'>Excellent Password!</span>";
    }
}

// Show/Hide Password
function togglePassword() {

    let passwordField =
        document.getElementById("password");

    if (passwordField.type === "password") {
        passwordField.type = "text";
    }
    else {
        passwordField.type = "password";
    }
}

// Generate Strong Password
function generatePassword() {

    const chars =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*";

    let password = "";

    for (let i = 0; i < 16; i++) {
        password += chars.charAt(
            Math.floor(Math.random() * chars.length)
        );
    }

    document.getElementById("password").value =
        password;

    checkPassword();
}
