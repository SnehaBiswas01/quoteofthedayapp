# quoteofthedayapp
index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quote of the Day</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="app-container">
    <h1>Quote of the Day</h1>
    <div id="quote-box">
      <p id="quote-text">Loading...</p>
      <span id="quote-author"></span>
    </div>
    <div class="buttons">
      <button onclick="newQuote()">Refresh Quote</button>
      <button onclick="saveFavorite()">❤ Save</button>
      <button onclick="shareQuote()">📤 Share</button>
    </div>
    <h2>Favorite Quotes</h2>
    <ul id="favorite-list"></ul>
  </div>

  <script src="script.js"></script>
</body>
</html>
style.css
body {
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(to right, #6dd5ed, #2193b0);
  color: #fff;
  margin: 0;
  padding: 0;
}

.app-container {
  max-width: 600px;
  margin: 50px auto;
  padding: 30px;
  background: rgba(0,0,0,0.3);
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.5);
  text-align: center;
}

#quote-box {
  font-size: 1.5rem;
  margin-bottom: 20px;
}

#quote-author {
  display: block;
  margin-top: 10px;
  font-style: italic;
  font-size: 1rem;
  color: #ffe;
}

.buttons button {
  margin: 10px;
  padding: 10px 20px;
  border: none;
  background-color: #fff;
  color: #2193b0;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
}

.buttons button:hover {
  background-color: #eee;
}

#favorite-list {
  list-style: none;
  padding: 0;
  margin-top: 20px;
  max-height: 150px;
  overflow-y: auto;
}

#favorite-list li {
  background-color: rgba(255, 255, 255, 0.1);
  margin: 5px 0;
  padding: 10px;
  border-radius: 8px;
  font-size: 0.9rem;
}
script.js
const quotes = [
  { text: "Believe you can and you're halfway there.", author: "Theodore Roosevelt" },
  { text: "You are never too old to set another goal or dream a new dream.", author: "C.S. Lewis" },
  { text: "Act as if what you do makes a difference. It does.", author: "William James" },
  { text: "Success is not final, failure is not fatal: It is the courage to continue that counts.", author: "Winston Churchill" },
  { text: "Happiness is not by chance, but by choice.", author: "Jim Rohn" }
];

let currentQuote = {};

function newQuote() {
  const randomIndex = Math.floor(Math.random() * quotes.length);
  currentQuote = quotes[randomIndex];
  document.getElementById("quote-text").innerText = "${currentQuote.text}";
  document.getElementById("quote-author").innerText = - ${currentQuote.author};
}

// Refresh on page load
window.onload = newQuote;

function saveFavorite() {
  const list = document.getElementById("favorite-list");
  const item = document.createElement("li");
  item.innerText = "${currentQuote.text}" — ${currentQuote.author};
  list.appendChild(item);
}

function shareQuote() {
  const message = "${currentQuote.text}" — ${currentQuote.author};
  if (navigator.share) {
    navigator.share({
      title: 'Quote of the Day',
      text: message
    }).catch(err => console.error("Sharing failed:", err));
  } else {
    alert("Sharing not supported on this browser. Copy the quote:\n\n" + message);
  }
}
