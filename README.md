# PRODIGY_AD_05
QR CODE SCANNER

index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>QR Code Scanner</title>
  <link rel="stylesheet" href="style.css" />
  <script src="https://unpkg.com/html5-qrcode" defer></script>
  <script src="script.js" defer></script>
</head>
<body>
  <div class="container">
    <h1>QR Code Scanner</h1>
    <div id="reader"></div>
    <p id="result">Scanned result will appear here</p>
    <button id="open-link" style="display:none;">Open Link</button>
  </div>
</body>
</html>

style.css
/* Import Google Font */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

body {
  font-family: 'Poppins', sans-serif;
  margin: 0;
  background: linear-gradient(135deg, #3a1c71, #d76d77, #ffaf7b);
  background-size: 400% 400%;
  animation: gradientBG 15s ease infinite;
  color: #fff;
}

@keyframes gradientBG {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.container {
  max-width: 500px;
  margin: 60px auto;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  padding: 30px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
  text-align: center;
}

h1 {
  font-weight: 600;
  font-size: 2em;
  margin-bottom: 20px;
  color: #fff;
}

#reader {
  width: 100%;
  border-radius: 10px;
  overflow: hidden;
  margin-bottom: 20px;
}

#result {
  font-size: 1.1em;
  background-color: rgba(0, 0, 0, 0.4);
  padding: 10px;
  border-radius: 10px;
}

#open-link {
  display: inline-block;
  margin-top: 20px;
  padding: 10px 25px;
  font-size: 1em;
  border: none;
  border-radius: 30px;
  background-color: #00b894;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

#open-link:hover {
  background-color: #019875;
}

script.js
document.addEventListener("DOMContentLoaded", function () {
  const resultElement = document.getElementById("result");
  const openLinkButton = document.getElementById("open-link");

  function onScanSuccess(decodedText, decodedResult) {
    resultElement.textContent = `Scanned Content: ${decodedText}`;

    if (decodedText.startsWith("http")) {
      openLinkButton.style.display = "inline-block";
      openLinkButton.onclick = () => window.open(decodedText, "_blank");
    } else {
      openLinkButton.style.display = "none";
    }

    // Stop scanning after success
    html5QrcodeScanner.clear();
  }

  const html5QrcodeScanner = new Html5QrcodeScanner("reader", {
    fps: 10,
    qrbox: 250,
  });

  html5QrcodeScanner.render(onScanSuccess);
});
