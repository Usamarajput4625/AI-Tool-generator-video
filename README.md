<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AI Video Generator</title>
  <style>
    body {
      font-family: sans-serif;
      padding: 40px;
      background: #f0f0f0;
      display: flex;
      justify-content: center;
    }
    .container {
      max-width: 600px;
      width: 100%;
      text-align: center;
    }
    textarea {
      width: 100%;
      height: 100px;
      margin-bottom: 20px;
    }
    select, button {
      margin: 10px;
      padding: 10px 20px;
    }
    #videoContainer {
      margin-top: 20px;
    }
    video {
      width: 100%;
      border-radius: 10px;
    }
    .download-btn {
      display: none;
      margin-top: 10px;
      background: green;
      color: white;
      padding: 10px 15px;
      border-radius: 6px;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>AI Video Generator</h2>
    <textarea id="prompt" placeholder="Enter your command (e.g., A cat dancing in rain)"></textarea>
    <br>
    <label>Select Ratio:</label>
    <select id="ratio">
      <option value="16-9">16:9</option>
      <option value="9-16">9:16</option>
    </select>
    <br>
    <button onclick="generateVideo()">Generate Video</button>

    <div id="videoContainer"></div>
    <a id="downloadBtn" class="download-btn" download="ai_video.mp4">Download Video</a>
  </div>

  <script>
    async function generateVideo() {
      const prompt = document.getElementById('prompt').value;
      const ratio = document.getElementById('ratio').value;

      if (!prompt) {
        alert("Please enter a prompt");
        return;
      }

      // Replace this with your actual backend endpoint
      const response = await fetch("https://your-backend.com/generate-video", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ prompt, ratio })
      });

      const data = await response.json();
      const videoUrl = data.videoUrl;

      const container = document.getElementById('videoContainer');
      container.innerHTML = `<video controls src="${videoUrl}"></video>`;

      const downloadBtn = document.getElementById('downloadBtn');
      downloadBtn.href = videoUrl;
      downloadBtn.style.display = "inline-block";
    }
  </script>
</body>
</html>
