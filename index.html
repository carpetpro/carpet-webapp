<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>پرو مجازی پیشرفته فرش</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; user-select: none; }
    body { font-family: Tahoma, sans-serif; background: #121212; color: #fff; text-align: center; overflow: hidden; }
    
    .controls { display: flex; gap: 6px; padding: 10px; background: #1e1e1e; justify-content: center; flex-wrap: wrap; z-index: 10; position: relative; }
    button, label.btn { padding: 8px 12px; border-radius: 8px; border: none; font-weight: bold; cursor: pointer; font-size: 12px; display: inline-flex; align-items: center; gap: 4px; }
    
    .btn-blue { background: #0088cc; color: #fff; }
    .btn-orange { background: #ff9800; color: #fff; }
    .btn-green { background: #4caf50; color: #fff; }
    .btn-purple { background: #9c27b0; color: #fff; }
    .btn-red { background: #f44336; color: #fff; }
    input[type="file"] { display: none; }

    /* نوار کاتالوگ فرش‌های نمونه */
    #catalog-bar { display: flex; gap: 8px; overflow-x: auto; padding: 8px; background: #252525; position: relative; z-index: 9; }
    #catalog-bar img { width: 50px; height: 50px; border-radius: 6px; border: 2px solid #444; object-fit: cover; cursor: pointer; flex-shrink: 0; }
    #catalog-bar img:active { border-color: #ff9800; }

    #canvas-container { position: relative; width: 100vw; height: calc(100vh - 130px); background: #181818; display: flex; align-items: center; justify-content: center; }
    canvas { display: block; max-width: 100%; max-height: 100%; touch-action: none; }

    #placeholder { position: absolute; top: 40%; left: 50%; transform: translate(-50%, -50%); color: #aaa; text-align: center; pointer-events: none; width: 85%; }
    #placeholder .icon { font-size: 45px; margin-bottom: 8px; display: block; }
  </style>
</head>
<body>

  <div class="controls">
    <label class="btn btn-blue">📁 گالری
      <input type="file" id="roomGalleryInput" accept="image/*">
    </label>
    <label class="btn btn-blue">📷 دوربین
      <input type="file" id="roomCameraInput" accept="image/*" capture="environment">
    </label>
    <label class="btn btn-orange">➕ افزودن فرش
      <input type="file" id="carpetInput" accept="image/*">
    </label>
    <button class="btn btn-purple" id="downloadBtn">💾 ذخیره عکس</button>
    <button class="btn btn-green" id="sendBtn">✅ ارسال به ربات</button>
  </div>

  <div id="catalog-bar">
    <span style="font-size:11px; align-self:center; color:#aaa; margin-left:4px;">نمونه‌ها:</span>
    <img src="https://picsum.photos/id/1062/200/200" title="فرش ۱" onclick="addCarpetFromUrl(this.src)">
    <img src="https://picsum.photos/id/1025/200/200" title="فرش ۲" onclick="addCarpetFromUrl(this.src)">
    <img src="https://picsum.photos/id/1040/200/200" title="فرش ۳" onclick="addCarpetFromUrl(this.src)">
  </div>

  <div id="canvas-container">
    <div id="placeholder">
      <span class="icon">🏠</span>
      <p><b>سامانه پرو مجازی فرش</b></p>
      <p style="font-size: 12px; margin-top: 6px; color: #888;">
        عکس اتاق را از دوربین یا گالری وارد کنید، سپس می‌توانید چند فرش اضافه کرده و زاویه آن‌ها را تنظیم کنید.
      </p>
    </div>
    <canvas id="mainCanvas"></canvas>
  </div>

<script>
  const tg = window.Telegram?.WebApp;
  if(tg) tg.expand();

  const canvas = document.getElementById('mainCanvas');
  const ctx = canvas.getContext('2d');
  const placeholder = document.getElementById('placeholder');

  let roomImg = null;
  let carpets = []; // آرایه نگهداری چند فرش هم‌زمان
  let activeCarpetIdx = -1;
  let activePtIdx = -1;

  function initCanvasSize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight - 130;
  }
  initCanvasSize();

  function handleRoomImage(file) {
    if (!file) return;
    const reader = new FileReader();
    reader.onload = (e) => {
      roomImg = new Image();
      roomImg.onload = () => {
        placeholder.style.display = 'none';
        canvas.width = roomImg.width;
        canvas.height = roomImg.height;
        draw();
      };
      roomImg.src = e.target.result;
    };
    reader.readAsDataURL(file);
  }

  document.getElementById('roomGalleryInput').addEventListener('change', (e) => handleRoomImage(e.target.files[0]));
  document.getElementById('roomCameraInput').addEventListener('change', (e) => handleRoomImage(e.target.files[0]));

  function addNewCarpet(imgObj) {
    const w = canvas.width;
    const h = canvas.height;
    const offset = carpets.length * 30; // فاصله دادن فرش‌های جدید از هم

    const newCarpet = {
      img: imgObj,
      pts: [
        { x: w * 0.3 + offset, y: h * 0.5 + offset },
        { x: w * 0.7 + offset, y: h * 0.5 + offset },
        { x: w * 0.8 + offset, y: h * 0.8 + offset },
        { x: w * 0.2 + offset, y: h * 0.8 + offset }
      ]
    };
    carpets.push(newCarpet);
    draw();
  }

  document.getElementById('carpetInput').addEventListener('change', (e) => {
    const file = e.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = (event) => {
      const img = new Image();
      img.onload = () => addNewCarpet(img);
      img.src = event.target.result;
    };
    reader.readAsDataURL(file);
  });

  function addCarpetFromUrl(url) {
    const img = new Image();
    img.crossOrigin = "anonymous";
    img.onload = () => addNewCarpet(img);
    img.src = url;
  }

  function drawPerspective(carpet) {
    const steps = 15;
    const { img, pts } = carpet;

    for (let i = 0; i < steps; i++) {
      for (let j = 0; j < steps; j++) {
        let u1 = i / steps, v1 = j / steps;
        let u2 = (i + 1) / steps, v2 = (j + 1) / steps;

        let p1 = getPoint(pts, u1, v1);
        let p2 = getPoint(pts, u2, v1);
        let p3 = getPoint(pts, u2, v2);
        let p4 = getPoint(pts, u1, v2);

        ctx.save();
        ctx.beginPath();
        ctx.moveTo(p1.x, p1.y);
        ctx.lineTo(p2.x, p2.y);
        ctx.lineTo(p3.x, p3.y);
        ctx.lineTo(p4.x, p4.y);
        ctx.closePath();
        ctx.clip();

        let sx = u1 * img.width;
        let sy = v1 * img.height;
        let sw = (u2 - u1) * img.width;
        let sh = (v2 - v1) * img.height;

        drawTriangle(img, p1, p2, p3, {x: sx, y: sy}, {x: sx + sw, y: sy}, {x: sx + sw, y: sy + sh});
        drawTriangle(img, p1, p3, p4, {x: sx, y: sy}, {x: sx + sw, y: sy + sh}, {x: sx, y: sy + sh});
        ctx.restore();
      }
    }
  }

  function getPoint(pts, u, v) {
    let topX = pts[0].x + u * (pts[1].x - pts[0].x);
    let topY = pts[0].y + u * (pts[1].y - pts[0].y);
    let botX = pts[3].x + u * (pts[2].x - pts[3].x);
    let botY = pts[3].y + u * (pts[2].y - pts[3].y);

    return { x: topX + v * (botX - topX), y: topY + v * (botY - topY) };
  }

  function drawTriangle(img, p0, p1, p2, t0, t1, t2) {
    let delta = t0.x * (t1.y - t2.y) + t1.x * (t2.y - t0.y) + t2.x * (t0.y - t1.y);
    if (Math.abs(delta) < 0.001) return;

    let deltaA = p0.x * (t1.y - t2.y) + p1.x * (t2.y - t0.y) + p2.x * (t0.y - t1.y);
    let deltaB = t0.x * (p1.x - p2.x) + t1.x * (p2.x - p0.x) + t2.x * (p0.x - p1.x);
    let deltaC = t0.x * (t1.y * p2.x - t2.y * p1.x) + t1.x * (t2.y * p0.x - t0.y * p2.x) + t2.x * (t0.y * p1.x - t1.y * p0.x);

    let deltaD = p0.y * (t1.y - t2.y) + p1.y * (t2.y - t0.y) + p2.y * (t0.y - t1.y);
    let deltaE = t0.x * (p1.y - p2.y) + t1.x * (p2.y - p0.y) + t2.x * (p0.y - p1.y);
    let deltaF = t0.x * (t1.y * p2.y - t2.y * p1.y) + t1.x * (t2.y * p0.y - t0.y * p2.y) + t2.x * (t0.y * p1.y - t1.y * p0.y);

    ctx.transform(deltaA / delta, deltaD / delta, deltaB / delta, deltaE / delta, deltaC / delta, deltaF / delta);
    ctx.drawImage(img, 0, 0);
  }

  function draw(hideHandles = false) {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    if (roomImg) ctx.drawImage(roomImg, 0, 0);

    carpets.forEach((carpet, cIdx) => {
      drawPerspective(carpet);

      if (!hideHandles) {
        ctx.strokeStyle = cIdx === activeCarpetIdx ? '#ff0055' : '#00e5ff';
        ctx.lineWidth = 2;
        ctx.beginPath();
        ctx.moveTo(carpet.pts[0].x, carpet.pts[0].y);
        carpet.pts.forEach(p => ctx.lineTo(p.x, p.y));
        ctx.closePath();
        ctx.stroke();

        carpet.pts.forEach(p => {
          ctx.fillStyle = cIdx === activeCarpetIdx ? '#ff0055' : '#00e5ff';
          ctx.beginPath();
          ctx.arc(p.x, p.y, canvas.width * 0.015, 0, Math.PI * 2);
          ctx.fill();
        });
      }
    });
  }

  function getCanvasPos(e) {
    const rect = canvas.getBoundingClientRect();
    const clientX = e.touches ? e.touches[0].clientX : e.clientX;
    const clientY = e.touches ? e.touches[0].clientY : e.clientY;
    return {
      x: (clientX - rect.left) * (canvas.width / rect.width),
      y: (clientY - rect.top) * (canvas.height / rect.height)
    };
  }

  function startDrag(e) {
    const pos = getCanvasPos(e);
    const radius = canvas.width * 0.06;

    activeCarpetIdx = -1;
    activePtIdx = -1;

    for (let c = carpets.length - 1; c >= 0; c--) {
      let pIdx = carpets[c].pts.findIndex(p => Math.hypot(p.x - pos.x, p.y - pos.y) < radius);
      if (pIdx !== -1) {
        activeCarpetIdx = c;
        activePtIdx = pIdx;
        break;
      }
    }
    draw();
  }

  function moveDrag(e) {
    if (activeCarpetIdx === -1 || activePtIdx === -1) return;
    const pos = getCanvasPos(e);
    carpets[activeCarpetIdx].pts[activePtIdx] = pos;
    draw();
  }

  function stopDrag() { activePtIdx = -1; }

  canvas.addEventListener('mousedown', startDrag);
  canvas.addEventListener('mousemove', moveDrag);
  canvas.addEventListener('mouseup', stopDrag);

  canvas.addEventListener('touchstart', startDrag);
  canvas.addEventListener('touchmove', moveDrag);
  canvas.addEventListener('touchend', stopDrag);

  // ذخیره تصویر روی دستگاه
  document.getElementById('downloadBtn').addEventListener('click', () => {
    if (!roomImg) return alert("لطفاً ابتدا عکس اتاق را وارد کنید.");
    draw(true);
    const link = document.createElement('a');
    link.download = 'carpet-pro.jpg';
    link.href = canvas.toDataURL('image/jpeg', 0.9);
    link.click();
    draw();
  });

  // ارسال تصویر به ربات تلگرام
  document.getElementById('sendBtn').addEventListener('click', () => {
    if (!roomImg) return alert("لطفاً ابتدا عکس اتاق را وارد کنید.");
    draw(true);
    const dataUrl = canvas.toDataURL('image/jpeg', 0.85);
    if (tg) tg.sendData(JSON.stringify({ image: dataUrl }));
    else alert("امکان ارسال وجود ندارد.");
    draw();
  });
</script>
</body>
</html>
