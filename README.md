
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Gift of Love</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Playfair+Display:ital,wght@0,500;0,600;1,400&family=Quicksand:wght@300;400;500&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: linear-gradient(135deg, #fff0f5, #f8d7e8);
      font-family: 'Quicksand', sans-serif;
      color: #d6006f;
      overflow-x: hidden;
      touch-action: pan-y;
      background-attachment: fixed;
    }

    /* === Título bonito === */
    .title {
      font-family: 'Dancing Script', cursive;
      font-size: 2.8rem;
      text-align: center;
      color: #e6007e;
      margin: 30px auto 15px;
      text-shadow: 
        0 0 10px rgba(255, 105, 180, 0.5),
        0 0 20px rgba(255, 105, 180, 0.3);
      position: relative;
      z-index: 2;
    }

    /* === Carta de Amor – Neón, doble borde, saturación === */
    .love-letter {
      width: 90%;
      max-width: 560px;
      margin: 20px auto 25px auto;
      padding: 32px 28px;
      background: rgba(255, 255, 255, 0.4);
      backdrop-filter: blur(12px);
      border-radius: 20px;
      border: 2px solid #ffb6c1;
      box-shadow: 
        0 0 0 4px rgba(255, 105, 180, 0.2),
        0 0 0 8px rgba(255, 105, 180, 0.1),
        0 10px 30px rgba(0, 0, 0, 0.15);
      position: relative;
      z-index: 2;
      text-align: center;
    }

    .love-letter h2 {
      font-family: 'Dancing Script', cursive;
      font-size: 2.4rem;
      color: #e6007e;
      margin-bottom: 14px;
      text-shadow: 0 0 8px rgba(255, 105, 180, 0.6);
    }

    .love-letter .content {
      font-family: 'Playfair Display', serif;
      font-size: 1.15rem;
      line-height: 1.9;
      color: #c20066;
      text-align: justify;
      max-width: 520px;
      margin: 0 auto;
      padding: 0 10px;
    }

    .love-letter .signature {
      font-family: 'Dancing Script', cursive;
      font-size: 1.8rem;
      color: #b2005d;
      margin-top: 20px;
      font-weight: 500;
    }

    /* === Contenedor 3D – más pequeño, neón === */
    .webgl-container {
      position: relative;
      width: 85%;
      height: 400px;
      margin: 20px auto 30px auto;
      border-radius: 18px;
      overflow: hidden;
      border: 2px solid #ffb6c1;
      box-shadow: 
        0 0 0 3px rgba(255, 105, 180, 0.2),
        0 8px 25px rgba(255, 105, 180, 0.2);
    }

    .webgl {
      position: absolute;
      top: 0;
      left: 0;
      width: 100% !important;
      height: 100% !important;
      outline: none;
      z-index: 1;
    }

    /* === Créditos – Cuadro pequeño y bonito === */
    .credits-container {
      text-align: center;
      margin: 15px auto 25px;
      width: 85%;
      max-width: 400px;
    }

    .credits {
      display: inline-block;
      padding: 8px 16px;
      background: rgba(255, 255, 255, 0.3);
      backdrop-filter: blur(6px);
      border-radius: 12px;
      border: 1px solid #ffb6c1;
      box-shadow: 
        0 0 0 2px rgba(255, 105, 180, 0.2),
        0 4px 12px rgba(255, 105, 180, 0.15);
      font-family: 'Quicksand', sans-serif;
      font-size: 0.8rem;
      color: #e6007e;
      font-weight: 500;
    }

    .credits a {
      color: #c20066;
      text-decoration: none;
      font-weight: 600;
    }

    .credits a:hover {
      text-decoration: underline;
    }

    /* === Lluvia de corazones === */
    #heart-rain {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 1;
    }
  </style>

  <!-- Shaders para neón -->
  <script type="x-shader/x-vertex" id="vertexshaderCandle">
    void main() {
      gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
    }
  </script>
  <script type="x-shader/x-fragment" id="fragmentshaderCandle">
    uniform float time;
    uniform float colorSpeed;
    uniform float delay;
    uniform vec3 baseColor;
    uniform vec3 finalColor;
    varying vec2 vUv;
    void main() {
      float t = mod(time - delay, colorSpeed) / colorSpeed;
      vec3 color = mix(baseColor, finalColor, t);
      gl_FragColor = vec4(color, 1.0);
    }
  </script>
</head>
<body>

  <!-- 🌟 Título -->
  <h1 class="title">Gift of Love</h1>

  <!-- 💌 Carta de Amor -->
  <div class="love-letter">
    <h2>Para Ti, Mi Vida</h2>
    <div class="content">
      Cada amanecer contigo es un milagro. 
      Cada mirada, una promesa. 
      Cada silencio, una canción que solo nosotros entendemos. 
      No necesito palabras para amarte, 
      porque mi alma ya te conoce desde antes de nacer. 
      Eres mi hogar, mi paz, mi eternidad.
    </div>
    <div class="signature">— Siempre tuyo 💞</div>
  </div>

  <!-- 🌀 3D Canvas (¡Giratorio manual!) -->
  <div class="webgl-container">
    <canvas class="webgl"></canvas>
  </div>

  <!-- ✨ Lluvia de corazones -->
  <canvas id="heart-rain"></canvas>

  <!-- 📜 Créditos en cuadro bonito -->
  <div class="credits-container">
    <p class="credits">
      by AnthZz Berrocal | BerMatMods<br>
      <a href="https://wa.me/51930569195" target="_blank">📩 Escríbeme</a>
    </p>
  </div>

  <script type="module">
    // ===== Lluvia de corazones animada =====
    const heartCanvas = document.getElementById('heart-rain');
    const ctx = heartCanvas.getContext('2d');
    let hearts = [];
    const emojis = ['❤️', '💖', '💗', '💕', '💓', '💘', '💝', '💞', '🫶', '🐝'];

    function resizeCanvas() {
      heartCanvas.width = window.innerWidth;
      heartCanvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    function createHeart() {
      return {
        x: Math.random() * heartCanvas.width,
        y: -20,
        emoji: Math.random() < 0.1 ? '🐝' : ['❤️', '💖', '💗', '💕', '💓'][Math.floor(Math.random() * 5)],
        size: Math.random() * 18 + 12,
        speed: Math.random() * 2.3 + 0.8,
        opacity: Math.random() * 0.9 + 0.3,
        vx: (Math.random() - 0.5) * 0.5, // Movimiento lateral suave
        floatOffset: Math.random() * Math.PI * 2 // Para flotar
      };
    }

    function animateHearts() {
      ctx.clearRect(0, 0, heartCanvas.width, heartCanvas.height);
      hearts = hearts.filter(h => h.y < heartCanvas.height + 20);
      if (hearts.length < 50) hearts.push(createHeart());
      hearts.forEach(h => {
        h.y += h.speed;
        h.x += h.vx;
        const float = Math.sin(Date.now() * 0.001 + h.floatOffset) * 2;
        ctx.font = `bold ${h.size}px Arial`;
        ctx.globalAlpha = h.opacity;
        ctx.fillText(h.emoji, h.x, h.y + float);
      });
      ctx.globalAlpha = 1;
      requestAnimationFrame(animateHearts);
    }
    animateHearts();

    // ===== Explosión de corazones al tocar =====
    document.body.addEventListener('click', (e) => {
      const particles = [];
      for (let i = 0; i < 40; i++) {
        const angle = Math.random() * Math.PI * 2;
        const speed = Math.random() * 5 + 2;
        particles.push({
          x: e.clientX,
          y: e.clientY,
          emoji: ['❤️', '💖', '💗', '💕', '💓', '💘', '💝', '💞', '🫶'][Math.floor(Math.random() * 9)],
          size: Math.random() * 24 + 10,
          vx: Math.cos(angle) * speed,
          vy: Math.sin(angle) * speed,
          life: 60
        });
      }

      function animateExplosion() {
        ctx.globalCompositeOperation = 'source-over';
        let stillAlive = false;
        particles.forEach(p => {
          if (p.life > 0) {
            ctx.font = `bold ${p.size}px Arial`;
            ctx.fillText(p.emoji, p.x, p.y);
            p.x += p.vx;
            p.y += p.vy;
            p.vy += 0.2;
            p.life--;
            stillAlive = true;
          }
        });
        if (stillAlive) requestAnimationFrame(animateExplosion);
      }
      animateExplosion();
    });

    // ===== Three.js Scene (¡sin cambios en el giro!) =====
    import * as THREE from "https://esm.sh/three@0.151.3";
    import { OrbitControls } from "https://esm.sh/three@0.151.3/addons/controls/OrbitControls.js";
    import { OutlineEffect } from "https://esm.sh/three@0.151.3/addons/effects/OutlineEffect.js";
    import { GLTFLoader } from "https://esm.sh/three@0.151.3/examples/jsm/loaders/GLTFLoader.js";

    const canvas = document.querySelector('canvas.webgl');
    const container = document.querySelector('.webgl-container');
    const scene = new THREE.Scene();
    const clock = new THREE.Clock();

    const sizes = {
      width: container.clientWidth,
      height: container.clientHeight
    };

    const camera = new THREE.PerspectiveCamera(10, sizes.width / sizes.height, 0.1, 1000);
    const controls = new OrbitControls(camera, canvas);
    let mixer;

    const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
    const effect = new OutlineEffect(renderer, {
      defaultThickness: 0.0014,
      defaultColor: [0.125, 0.125, 0.125],
      defaultAlpha: 1
    });
    renderer.setSize(sizes.width, sizes.height);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

    // ===== Luces =====
    const ambientLight = new THREE.AmbientLight("#ffffff", 0.9);
    scene.add(ambientLight);
    const directionalLight = new THREE.DirectionalLight('#ffffff', 0.35);
    directionalLight.position.set(-2, 5, 0);
    scene.add(directionalLight);

    // ===== Controles – Giro Manual 100% =====
    controls.enableDamping = true;
    controls.dampingFactor = 0.05;
    controls.rotateSpeed = 0.7;
    controls.enableZoom = true;
    controls.enablePan = true;
    controls.minPolarAngle = Math.PI / 5;
    controls.maxPolarAngle = Math.PI / 2;
    controls.minDistance = 20;
    controls.maxDistance = 47;

    // ===== Cámara =====
    camera.position.set(35, 8, 36);
    scene.add(camera);

    // ===== Materiales (igual que original) =====
    const textureLoader = new THREE.TextureLoader();
    const bakedTexture = textureLoader.load('https://rawcdn.githack.com/ricardoolivaalonso/threejs-journey01/e3cfc35a8270972a21435ad885da2bab54ec2d11/baked.jpg');
    bakedTexture.flipY = false;

    const bakedMaterial = new THREE.MeshStandardMaterial({ map: bakedTexture, side: THREE.DoubleSide, roughness: 0.5 });
    const snowMaterial = new THREE.MeshPhysicalMaterial({ color: 0xeeeeee, roughness: 0.6, metalness: 0.1 });
    const windowMaterial = new THREE.MeshBasicMaterial({ color: 0xFFDCC2, side: THREE.DoubleSide });
    const neonBaseMaterial = new THREE.MeshStandardMaterial({ emissive: 0xffffff, side: THREE.DoubleSide });

    const neonMaterial = new THREE.ShaderMaterial({
      uniforms: {
        time: { value: 1.0 },
        delay: { value: 0.0 },
        colorSpeed: { value: 5.0 },
        baseColor: { value: new THREE.Color(0x9bcab6) },
        finalColor: { value: new THREE.Color(0xffffff) }
      },
      vertexShader: document.getElementById('vertexshaderCandle').textContent,
      fragmentShader: document.getElementById('fragmentshaderCandle').textContent
    });

    const neonMaterial2 = new THREE.ShaderMaterial({
      uniforms: {
        time: { value: 1.0 },
        delay: { value: 0.0 },
        colorSpeed: { value: 5.0 },
        baseColor: { value: new THREE.Color(0xe39f9f) },
        finalColor: { value: new THREE.Color(0xffffff) }
      },
      vertexShader: document.getElementById('vertexshaderCandle').textContent,
      fragmentShader: document.getElementById('fragmentshaderCandle').textContent
    });

    const fireMaterial = new THREE.MeshPhongMaterial({ color: 0xffdab9, side: THREE.DoubleSide });

    // ===== Cargar modelos =====
    const gltfLoader = new GLTFLoader();

    gltfLoader.load('https://rawcdn.githack.com/ricardoolivaalonso/threejs-journey01/e3cfc35a8270972a21435ad885da2bab54ec2d11/model.glb', (gltf) => {
      gltf.scene.traverse(child => child.material = bakedMaterial);
      gltf.scene.position.set(0, -0.3, 0);
      scene.add(gltf.scene);
    });

    gltfLoader.load('https://rawcdn.githack.com/ricardoolivaalonso/threejs-journey01/e3cfc35a8270972a21435ad885da2bab54ec2d11/model2.glb', (gltf) => {
      gltf.scene.traverse(child => {
        if (child.material) {
          switch (child.material.name) {
            case 'SnowSimple': child.material = snowMaterial; break;
            case 'Window': child.material = windowMaterial; break;
            case 'NeonBase': child.material = neonBaseMaterial; break;
            case 'Neon.001': child.material = neonMaterial2; break;
            case 'Neon': child.material = neonMaterial; break;
            case 'Fire': child.material = fireMaterial; break;
          }
        }
      });
      scene.add(gltf.scene);
      gltf.scene.position.set(0, -0.3, 0);
      if (gltf.animations.length > 0) {
        mixer = new THREE.AnimationMixer(gltf.scene);
        gltf.animations.forEach(clip => mixer.clipAction(clip).play());
      }
    });

    // ===== Fuego (partículas) =====
    const cube = new THREE.Mesh(new THREE.BoxGeometry(1, 0.01, 0.5), new THREE.MeshStandardMaterial({ color: 0xffffff }));
    cube.position.set(0.1, -2.2, -1.6);
    scene.add(cube);

    function getParticleSystem(params) {
      const { camera, emitter, parent, rate, texture } = params;
      const uniforms = {
        diffuseTexture: { value: new THREE.TextureLoader().load(texture) },
        pointMultiplier: { value: window.innerHeight / (2.0 * Math.tan(30.0 * Math.PI / 180.0)) }
      };
      const material = new THREE.ShaderMaterial({
        uniforms: uniforms,
        vertexShader: `
          uniform float pointMultiplier;
          attribute float size;
          attribute float angle;
          attribute vec4 aColor;
          varying vec4 vColor;
          varying vec2 vAngle;
          void main() {
            vec4 mvPosition = modelViewMatrix * vec4(position, 1.0);
            gl_Position = projectionMatrix * mvPosition;
            gl_PointSize = size * pointMultiplier / gl_Position.w;
            vAngle = vec2(cos(angle), sin(angle));
            vColor = aColor;
          }
        `,
        fragmentShader: `
          uniform sampler2D diffuseTexture;
          varying vec4 vColor;
          varying vec2 vAngle;
          void main() {
            vec2 coords = (gl_PointCoord - 0.5) * mat2(vAngle.x, vAngle.y, -vAngle.y, vAngle.x) + 0.5;
            gl_FragColor = texture2D(diffuseTexture, coords) * vColor;
          }
        `,
        transparent: true,
        blending: THREE.AdditiveBlending,
        depthTest: true,
        vertexColors: true
      });

      const geometry = new THREE.BufferGeometry();
      ['position', 'size', 'aColor', 'angle'].forEach(attr => {
        geometry.setAttribute(attr, new THREE.Float32BufferAttribute([], attr === 'position' ? 3 : 1));
      });

      const points = new THREE.Points(geometry, material);
      parent.add(points);
      let particles = [];

      return {
        update: (dt) => {
          const n = Math.floor(dt * rate);
          for (let i = 0; i < n; i++) {
            const life = (Math.random() * 0.75 + 0.25) * 1.5;
            particles.push({
              position: new THREE.Vector3(
                (Math.random() * 1.5 - 1) * 0.5,
                (Math.random() * 0.125 - 1) * 0.5,
                (Math.random() * 1.5 - 1) * 0.5
              ).add(emitter.position),
              size: (Math.random() * 0.5 + 0.5) * 3.0,
              colour: new THREE.Color(),
              alpha: 1,
              life: life,
              maxLife: life,
              rotation: Math.random() * 2 * Math.PI,
              rotationRate: Math.random() * 0.01 - 0.005,
              velocity: new THREE.Vector3(0, 1.5, 0),
              currentSize: 0
            });
          }

          particles = particles.filter(p => (p.life -= dt) > 0);
          particles.forEach(p => {
            const t = 1 - p.life / p.maxLife;
            p.rotation += p.rotationRate;
            p.alpha = t < 0.4 ? t / 0.4 : 1;
            p.currentSize = p.size * t;
            p.colour.setRGB(1, 1 - t * 0.5, 1 - t);
            p.position.add(p.velocity.clone().multiplyScalar(dt));
            const drag = p.velocity.clone().multiplyScalar(dt * 0.1);
            ['x','y','z'].forEach(a => {
              const d = Math.min(Math.abs(drag[a]), Math.abs(p.velocity[a]));
              drag[a] = Math.sign(p.velocity[a]) * d;
            });
            p.velocity.sub(drag);
          });

          particles.sort((a, b) => camera.position.distanceTo(b.position) - camera.position.distanceTo(a.position));

          ['position','size','aColor','angle'].forEach((attr, i) => {
            const values = [];
            particles.forEach(p => {
              const v = { position: [p.position.x, p.position.y, p.position.z], size: [p.currentSize], aColor: [p.colour.r, p.colour.g, p.colour.b, p.alpha], angle: [p.rotation] }[attr];
              values.push(...v);
            });
            const itemSize = { position: 3, size: 1, aColor: 4, angle: 1 }[attr];
            geometry.setAttribute(attr, new THREE.Float32BufferAttribute(values, itemSize));
            geometry.attributes[attr].needsUpdate = true;
          });
        }
      };
    }

    const fireEffect = getParticleSystem({
      camera,
      emitter: cube,
      parent: scene,
      rate: 200,
      texture: 'https://rawcdn.githack.com/ricardoolivaalonso/threejs-journey01/e3cfc35a8270972a21435ad885da2bab54ec2d11/fire.png'
    });

    // ===== Loop principal (¡controls.update() incluido!) =====
    const tick = () => {
      requestAnimationFrame(tick);
      const delta = clock.getDelta();
      if (mixer) mixer.update(delta);

      controls.update(); // ✅ Giro manual activo
      if (neonMaterial.uniforms) neonMaterial.uniforms.time.value += 0.075;
      if (neonMaterial2.uniforms) neonMaterial2.uniforms.time.value += 0.09;
      fireEffect.update(0.016);
      effect.render(scene, camera);
    };

    window.addEventListener('resize', () => {
      sizes.width = container.clientWidth;
      sizes.height = container.clientHeight;
      camera.aspect = sizes.width / sizes.height;
      camera.updateProjectionMatrix();
      renderer.setSize(sizes.width, sizes.height);
      resizeCanvas();
    });

    tick();
  </script>
</body>
</html>
