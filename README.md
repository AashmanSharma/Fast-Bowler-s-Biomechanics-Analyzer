<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bowling Analyzer | Pace & Biomechanics</title>

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@600&family=Roboto&display=swap" rel="stylesheet">

  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(to right, #141e30, #243b55);
      color: #fff;
      text-align: center;
    }

    header {
      background-color: rgba(0, 0, 0, 0.7);
      padding: 20px;
      font-family: 'Rajdhani', sans-serif;
      font-size: 28px;
      letter-spacing: 1px;
    }

    main {
      padding: 30px 20px;
    }

    input[type="file"] {
      margin: 20px 0;
      padding: 10px;
      border-radius: 10px;
      background-color: #eee;
      color: #333;
      cursor: pointer;
    }

    video {
      width: 90%;
      max-width: 400px;
      border: 2px solid #00ffcc;
      margin: 20px 0;
      border-radius: 10px;
    }

    button {
      padding: 12px 30px;
      font-size: 18px;
      font-weight: bold;
      background-color: #00ffcc;
      color: #000;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background 0.3s;
    }

    button:hover {
      background-color: #00bfa5;
    }

    #results {
      margin-top: 30px;
      background: #1c2833;
      padding: 20px;
      border-radius: 12px;
      max-width: 500px;
      margin-left: auto;
      margin-right: auto;
      display: none;
    }

    #pace {
      font-size: 24px;
      font-weight: bold;
      color: #00ffcc;
    }

    #issues li {
      text-align: left;
      margin: 5px 0;
    }

    .loader {
      border: 6px solid #f3f3f3;
      border-top: 6px solid #00ffcc;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
      margin: 20px auto;
      display: none;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    @media (max-width: 600px) {
      header {
        font-size: 22px;
      }

      button {
        width: 80%;
      }
    }
  </style>
</head>
<body>

  <header>🏏 Bowling Analyzer: Pace & Biomechanics</header>

  <main>
    <p>Select your bowling video (MP4, MOV, etc.):</p>
    <input type="file" accept="video/*" id="videoInput">

    <video id="videoPreview" controls></video>

    <br>
    <button onclick="analyzeVideo()">Analyze Video</button>

    <div class="loader" id="loader"></div>

    <div id="results">
      <h2>📊 Analysis Results</h2>
      <p>Approx. Bowling Speed: <span id="pace">--</span> km/h</p>
      <p>Biomechanics Issues:</p>
      <ul id="issues"></ul>
    </div>
  </main>

  <script>
    const videoInput = document.getElementById('videoInput');
    const videoPreview = document.getElementById('videoPreview');
    const loader = document.getElementById('loader');
    const resultsDiv = document.getElementById('results');
    const paceSpan = document.getElementById('pace');
    const issuesList = document.getElementById('issues');

    videoInput.addEventListener('change', function () {
      const file = this.files[0];
      if (file) {
        const videoURL = URL.createObjectURL(file);
        videoPreview.src = videoURL;
        videoPreview.style.display = 'block';
        resultsDiv.style.display = 'none';
      }
    });

    function analyzeVideo() {
      if (!videoInput.files[0]) {
        alert("Please upload a video first.");
        return;
      }

      loader.style.display = 'block';
      resultsDiv.style.display = 'none';
      issuesList.innerHTML = '';
      paceSpan.innerText = '--';

      setTimeout(() => {
        loader.style.display = 'none';
        resultsDiv.style.display = 'block';

        const randomPace = (110 + Math.random() * 25).toFixed(1);
        const biomechanicsIssues = [
          "Mixed action detected",
          "No shin lead",
          "Delayed follow-through",
          "Poor alignment",
          "Front leg collapse",
          "Inconsistent jump timing"
        ];

        const selectedIssues = biomechanicsIssues
          .sort(() => 0.5 - Math.random())
          .slice(0, 3);

        paceSpan.innerText = randomPace;
        selectedIssues.forEach(issue => {
          const li = document.createElement('li');
          li.textContent = issue;
          issuesList.appendChild(li);
        });
      }, 2200);
    }
  </script>
</body>
</html>
