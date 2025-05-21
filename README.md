# StockScope
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>StockScope - Live Stock Tracker</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #0a0a0a;
      color: #e0e0e0;
    }
    nav {
      background-color: #111;
      padding: 1rem;
      display: flex;
      justify-content: space-around;
      position: sticky;
      top: 0;
    }
    nav a {
      color: #0ff;
      text-decoration: none;
      font-weight: bold;
    }
    nav a:hover {
      text-decoration: underline;
    }
    section {
      padding: 2rem;
      max-width: 800px;
      margin: auto;
    }
    h1, h2 {
      color: #0ff;
    }
    .card {
      background-color: #1a1a1a;
      padding: 1.5rem;
      margin-top: 1rem;
      border-radius: 10px;
      box-shadow: 0 0 10px #0ff3;
    }
    input, button {
      padding: 0.5rem 1rem;
      font-size: 1rem;
      margin-top: 1rem;
      border: none;
      border-radius: 5px;
    }
    input {
      width: 150px;
      margin-right: 0.5rem;
    }
    button {
      background-color: #0ff;
      color: #000;
      cursor: pointer;
    }
    button:hover {
      background-color: #00cccc;
    }
  </style>
</head>
<body>
  <nav>
    <a href="#home">Home</a>
    <a href="#prices">Track Stocks</a>
    <a href="#about">About</a>
  </nav>

  <section id="home">
    <h1>Welcome to StockScope</h1>
    <p>Track live stock prices in real time. Enter any stock symbol (e.g., AAPL, MSFT, TSLA).</p>
  </section>

  <section id="prices">
    <h2>Live Stock Price Lookup</h2>
    <input type="text" id="stockSymbol" placeholder="Enter symbol" />
    <button onclick="fetchStock()">Track</button>

    <div class="card" id="stockCard" style="display:none;">
      <h3 id="stockName"></h3>
      <p>Current Price: $<span id="stockPrice">Loading...</span></p>
    </div>
  </section>

  <section id="about">
    <h2>About</h2>
    <p>This site fetches real-time stock prices using the Twelve Data API. It's simple, fast, and free to use.</p>
  </section>

  <script>
    async function fetchStock() {
      const symbol = document.getElementById('stockSymbol').value.toUpperCase();
      const apiKey = "YOUR_API_KEY_HERE";
      const url = `https://api.twelvedata.com/price?symbol=${symbol}&apikey=${apiKey}`;

      document.getElementById('stockCard').style.display = 'block';
      document.getElementById('stockName').innerText = `${symbol} Stock Price`;
      document.getElementById('stockPrice').innerText = 'Loading...';

      try {
        const response = await fetch(url);
        const data = await response.json();

        if (data.price) {
          document.getElementById('stockPrice').innerText = data.price;
        } else {
          document.getElementById('stockPrice').innerText = "Invalid symbol or API limit reached.";
        }
      } catch (error) {
        document.getElementById('stockPrice').innerText = "Error fetching data.";
        console.error(error);
      }
    }
  </script>
</body>
</html>
