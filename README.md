# Blog-de-L-D
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>El blog de L&D</title>
  <link href="https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap" rel="stylesheet" />
  <style>
    body {
      font-family: 'Indie Flower', cursive;
      margin: 0;
      background: #fce4ec;
      color: #333;
      overflow-x: hidden;
    }

    header {
      background-color: #82b1ff;
      color: white;
      padding: 30px;
      text-align: center;
    }

    header h1 {
      margin: 0;
      font-size: 3em;
    }

    .intro {
      background-color: #fff0f6;
      color: #ec407a;
      padding: 20px;
      text-align: center;
      font-size: 1.4em;
      border-bottom: 2px dashed #ec407a;
    }

    main {
      padding: 20px;
      max-width: 800px;
      margin: auto;
    }

    .card {
      background-color: white;
      padding: 20px;
      border-radius: 12px;
      margin-bottom: 20px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      position: relative;
    }

    .card h2, .card h3 {
      color: #ec407a;
    }

    .card input, .card textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 2px solid #ec407a;
      border-radius: 8px;
      font-family: 'Indie Flower', cursive;
      font-size: 1em;
    }

    .card button {
      background-color: #82b1ff;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 1em;
      transition: 0.3s;
    }

    .card button:hover {
      background-color: #5c8df6;
    }

    video {
      width: 100%;
      border-radius: 12px;
      margin-top: 10px;
    }

    footer {
      background-color: #f8bbd0;
      color: #333;
      text-align: center;
      padding: 20px;
      margin-top: 40px;
      padding-bottom: 60px;
    }

    .likes {
      margin-top: 12px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .likes button {
      background-color: #ec407a;
      border: none;
      border-radius: 20px;
      padding: 6px 14px;
      color: white;
      font-weight: bold;
      cursor: pointer;
      transition: background-color 0.3s;
      font-family: 'Indie Flower', cursive;
    }

    .likes button:hover {
      background-color: #b81d55;
    }

    .likes span {
      font-size: 1.2em;
      font-weight: bold;
      color: #ec407a;
      user-select: none;
    }

    /* Decoraciones fijas */
    .decoracion {
      position: fixed;
      z-index: 1;
      width: 70px;
      opacity: 0.85;
      pointer-events: none;
    }

    .img1 {
      bottom: 10px;
      left: 10px;
    }

    .img2 {
      top: 10px;
      right: 10px;
    }

    .img3 {
      bottom: 20px;
      right: 20px;
    }
  </style>
</head>
<body>

  <header>
    <h1>El blog de L&D</h1>
  </header>

  <div class="intro">
    Hola, somos <strong>Lore y Dann</strong> y este es nuestro día a día
  </div>

  <main>
    <div class="card">
      <h2>Publicar una nota</h2>
      <input type="text" placeholder="Título de tu nota" id="notaTitulo" />
      <textarea rows="5" placeholder="Escribe aquí tu reflexión, actualización o aprendizaje..." id="notaTexto"></textarea>
      <button onclick="publicarNota()">Publicar</button>
    </div>

    <div class="card">
      <h2>Subir video</h2>
      <input type="file" accept="video/*" onchange="previewVideo(event)" />
      <video id="videoPreview" controls hidden></video>
    </div>

    <div id="notasPublicadas"></div>
  </main>

  <footer>
    &copy; 2025 El blog de L&D. Hecho con cariño por Lore y Dann.
  </footer>

  <!-- Decoraciones con tus imágenes -->
  <img src="https://i.imgur.com/bto0DVv.jpg" class="decoracion img1" alt="decoración 1" />
  <img src="https://i.imgur.com/2hA4ckQ.jpg" class="decoracion img2" alt="decoración 2" />
  <img src="https://i.imgur.com/U95ohVH.jpg" class="decoracion img3" alt="decoración 3" />

  <script>
    function previewVideo(event) {
      const file = event.target.files[0];
      if (file) {
        const video = document.getElementById('videoPreview');
        video.src = URL.createObjectURL(file);
        video.hidden = false;
      }
    }

    function publicarNota() {
      const titulo = document.getElementById('notaTitulo').value.trim();
      const texto = document.getElementById('notaTexto').value.trim();
      if(!titulo || !texto) {
        alert('Por favor, ingresa título y texto para la nota.');
        return;
      }

      const notasContainer = document.getElementById('notasPublicadas');

      const notaDiv = document.createElement('div');
      notaDiv.className = 'card';

      notaDiv.innerHTML = `
        <h3>${escapeHtml(titulo)}</h3>
        <p>${escapeHtml(texto).replace(/\n/g, '<br>')}</p>
        <div class="likes">
          <button onclick="darLike(this)">Me gusta ❤️</button>
          <span>0</span>
        </div>
      `;

      notasContainer.prepend(notaDiv);

      document.getElementById('notaTitulo').value = '';
      document.getElementById('notaTexto').value = '';
    }

    function darLike(boton) {
      const contador = boton.nextElementSibling;
      let likes = parseInt(contador.textContent);
      contador.textContent = likes + 1;
    }

    function escapeHtml(text) {
      const div = document.createElement('div');
      div.textContent = text;
      return div.innerHTML;
    }
  </script>
</body>
