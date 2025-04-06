# fng-widget
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Fear & Greed Index</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #111;
      color: #32ff00;
      text-align: center;
      padding: 20px;
    }
    .loading {
      font-size: 22px;
    }
    .value {
      font-size: 32px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div id="fng-container" class="loading">Loading Fear & Greed Index...</div>

  <script>
    fetch("https://api.codetabs.com/v1/proxy/?quest=https://money.cnn.com/data/fear-and-greed/")
      .then(response => response.text())
      .then(html => {
        const parser = new DOMParser();
        const doc = parser.parseFromString(html, "text/html");
        const match = doc.body.textContent.match(/Fear & Greed Now: (\d+)/i);

        const container = document.getElementById("fng-container");
        if (match && match[1]) {
          container.innerHTML = `<div class="value">CNN Fear & Greed Index: ${match[1]}</div>`;
        } else {
          container.innerHTML = "Unable to fetch index value.";
        }
      })
      .catch(() => {
        document.getElementById("fng-container").innerText = "Error loading index.";
      });
  </script>
</body>
</html>
