<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Timeless Love Story</title>
    <style>
        body {
            font-family: 'Georgia', serif;
            background: linear-gradient(to bottom, #ffe6f2, #ffb3ba);
            color: #333;
            text-align: center;
            padding: 50px;
            margin: 0;
            overflow-x: hidden;
        }
        .signup, .login {
            max-width: 400px;
            margin: auto;
            background: rgba(255, 255, 255, 0.9);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        .container {
            max-width: 700px;
            margin: auto;
            background: rgba(255, 255, 255, 0.9);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            animation: fadeIn 2s ease-in;
            display: none; /* Hidden until login */
        }
        .admin-panel {
            max-width: 600px;
            margin: auto;
            background: rgba(255, 255, 255, 0.9);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            display: none; /* Hidden unless admin */
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        h1 {
            color: #d32f2f;
            font-size: 2.5em;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        .story {
            font-size: 18px;
            line-height: 1.6;
            margin-bottom: 30px;
        }
        .heart {
            font-size: 3em;
            color: #e91e63;
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        .quiz {
            margin-top: 30px;
        }
        .question {
            font-size: 20px;
            margin-bottom: 20px;
        }
        .quiz input {
            width: 80%;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            margin-bottom: 10px;
        }
        .buttons {
            margin-top: 30px;
            display: none; /* Hidden until quiz completes */
        }
        button {
            padding: 15px 30px;
            margin: 0 15px;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .yes {
            background: linear-gradient(45deg, #4CAF50, #66BB6A);
            color: white;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        .yes:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 12px rgba(0,0,0,0.3);
        }
        .no {
            background: linear-gradient(45deg, #f44336, #e57373);
            color: white;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        .no:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 12px rgba(0,0,0,0.3);
        }
        .persuasion {
            display: none;
            margin-top: 20px;
            font-size: 18px;
            color: #d32f2f;
            font-style: italic;
        }
        .message-form {
            margin-top: 30px;
            display: none; /* Show after yes */
        }
        .message-form textarea {
            width: 100%;
            height: 100px;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        .message-form button {
            margin-top: 10px;
            background: #2196F3;
            color: white;
        }
        .footer {
            margin-top: 40px;
            font-style: italic;
            color: #666;
        }
        input {
            padding: 10px;
            margin: 10px 0;
            width: 100%;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        .switch {
            margin-top: 20px;
            cursor: pointer;
            color: #2196F3;
        }
        .admin-link {
            position: fixed;
            bottom: 10px;
            right: 10px;
            background: #333;
            color: white;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
        }
    </style>
    <script>
        let step = 0;
        let quizAnswers = [];
        const questions = [
            "What is your favorite thing about our relationship?",
            "Describe a moment when you felt most loved by me.",
            "What does forever mean to you with me?"
        ];

        // Check if user is already signed up
        window.onload = function() {
            if (localStorage.getItem('phone')) {
                showLogin();
            } else {
                showSignup();
            }
        };

        function showSignup() {
            document.querySelector('.signup').style.display = 'block';
            document.querySelector('.login').style.display = 'none';
            document.querySelector('.container').style.display = 'none';
            document.querySelector('.admin-panel').style.display = 'none';
        }

        function showLogin() {
            document.querySelector('.signup').style.display = 'none';
            document.querySelector('.login').style.display = 'block';
            document.querySelector('.container').style.display = 'none';
            document.querySelector('.admin-panel').style.display = 'none';
        }

        function signup() {
            const phone = document.getElementById('signup-phone').value.trim();
            const password = document.getElementById('signup-password').value;
            if (phone && password) {
                localStorage.setItem('phone', phone);
                localStorage.setItem('password', password);
                alert('Signup successful! Now log in.');
                showLogin();
            } else {
                alert('Please enter phone and password.');
            }
        }

        function login() {
            const phone = document.getElementById('login-phone').value.trim();
            const password = document.getElementById('login-password').value;
            const storedPhone = localStorage.getItem('phone');
            const storedPassword = localStorage.getItem('password');
            if (phone === storedPhone && password === storedPassword) {
                document.querySelector('.login').style.display = 'none';
                document.querySelector('.container').style.display = 'block';
            } else {
                alert('Invalid phone or password! Try again.');
            }
        }

        function nextQuestion() {
            const answer = document.getElementById('quiz-answer').value.trim();
            if (answer) {
                quizAnswers.push({ question: questions[step], answer: answer });
                step++;
                if (step < questions.length) {
                    document.querySelector('.question').textContent = questions[step];
                    document.getElementById('quiz-answer').value = '';
                } else {
                    document.querySelector('.quiz').style.display = 'none';
                    document.querySelector('.buttons').style.display = 'block';
                }
            } else {
                alert('Please enter an answer.');
            }
        }

        function handleYes() {
            alert('Forever starts now! I love you endlessly!');
            document.querySelector('.message-form').style.display = 'block';
        }

        function handleNo() {
            document.querySelector('.persuasion').style.display = 'block';
            document.querySelector('.buttons').style.display = 'block'; // Show buttons again for retry
            alert('Think of our beautiful future together—adventures, laughter, and endless love. Let\'s try again!');
        }

        function sendMessage() {
            const message = document.querySelector('textarea').value;
            if (message.trim()) {
                // Save to local storage (simulate database)
                let submissions = JSON.parse(localStorage.getItem('submissions')) || [];
                const phone = localStorage.getItem('phone');
                submissions.push({
                    phone: phone,
                    quizAnswers: quizAnswers,
                    message: message,
                    timestamp: new Date().toLocaleString()
                });
                localStorage.setItem('submissions', JSON.stringify(submissions));
                alert('Message sent! Thank you.');
                document.querySelector('textarea').value = '';
            } else {
                alert('Please enter a message.');
            }
        }

        function showAdminPanel() {
            const adminPassword = prompt('Enter admin password:');
            if (adminPassword === 'iloveyoushital') {
                document.querySelector('.signup').style.display = 'none';
                document.querySelector('.login').style.display = 'none';
                document.querySelector('.container').style.display = 'none';
                document.querySelector('.admin-panel').style.display = 'block';
                displaySubmissions();
            } else {
                alert('Invalid admin password.');
            }
        }

        function displaySubmissions() {
            const submissions = JSON.parse(localStorage.getItem('submissions')) || [];
            const submissionList = document.getElementById('submission-list');
            submissionList.innerHTML = '';
            if (submissions.length === 0) {
                submissionList.innerHTML = '<p>No submissions yet.</p>';
            } else {
                submissions.forEach((sub, index) => {
                    const div = document.createElement('div');
                    div.innerHTML = `
                        <strong>Submission ${index + 1} (${sub.timestamp}):</strong><br>
                        <strong>Phone:</strong> ${sub.phone}<br>
                        <strong>Quiz Answers:</strong><br>
                        ${sub.quizAnswers.map(ans => `${ans.question} - ${ans.answer}`).join('<br>')}<br>
                        <strong>Message:</strong> ${sub.message}<hr>
                    `;
                    submissionList.appendChild(div);
                });
            }
        }

        function backToSite() {
            document.querySelector('.admin-panel').style.display = 'none';
            if (localStorage.getItem('phone')) {
                showLogin();
            } else {
                showSignup();
            }
        }
    </script>
</head>
<body>
    <div class="signup">
        <h1>Sign Up to View Your Surprise</h1>
        <p>Create an account with your phone number and password:</p>
        <input type="tel" id="signup-phone" placeholder="Phone Number (e.g., +1234567890)">
        <input type="password" id="signup-password" placeholder="Password">
        <button onclick="signup()">Sign Up</button>
        <p class="switch" onclick="showLogin()">Already have an account? Log in</p>
    </div>
    <div class="login">
        <h1>Login to View Your Surprise</h1>
        <p>Enter your phone number and password:</p>
        <input type="tel" id="login-phone" placeholder="Phone Number">
        <input type="password" id="login-password" placeholder="Password">
        <button onclick="login()">Login</button>
        <p class="switch" onclick="showSignup()">Need to sign up?</p>
    </div>
    <div class="container">
        <h1>My Eternal Flame</h1>
        <div class="story">
            <p>In the quiet whispers of the night, under a canopy of stars that pale in comparison to your eyes, I found my forever. Every beat of my heart echoes your name, a symphony of love that knows no end.</p>
            <p>You've turned my world into a garden of roses, where every petal blooms with the promise of tomorrow. With you, I've discovered the true meaning of passion, tenderness, and unbreakable bonds.</p>
            <p>Today, as the sun sets on our shared dreams, I kneel before you—not just in body, but in soul. Will you join me in this grand adventure, hand in hand, heart to heart?</p>
            <p>And now, to make this moment even more magical, let's play a little game of love...</p>
        </div>
        <div class="heart">❤️</div>
        <div class="quiz">
            <div class="question">What is your favorite thing about our relationship?</div>
            <input type="text" id="quiz-answer" placeholder="Your answer...">
            <button onclick="nextQuestion()">Next</button>
        </div>
        <div class="buttons">
            <button class="yes" onclick="handleYes()">Yes, My Love!</button>
            <button class="no" onclick="handleNo()">No... But Maybe?</button>
        </div>
        <div class="persuasion">
            <p>Imagine our beautiful future: waking up together every morning, exploring new places, building a life filled with joy and love. You're my everything—let's say yes to forever!</p>
        </div>
        <div class="message-form">
            <p>Leave me a follow-up message:</p>
            <textarea placeholder="Your thoughts..."></textarea>
            <button onclick="sendMessage()">Send</button>
        </div>
        <p class="footer">Your love story deserves the spotlight!</p>
    </div>
    <div class="admin-panel">
        <h1>Admin Panel</h1>
        <p>View all submitted data:</p>
        <div id="submission-list"></div>
        <button onclick="backToSite()">Back to Site</button>
    </div>
    <div class="admin-link" onclick="showAdminPanel()">Admin</div>
</body>
</html>
