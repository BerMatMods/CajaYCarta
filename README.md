
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Gift of Love</title>

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@500;600&display=swap" rel="stylesheet">

  <!-- Animate.css -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" />

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background-color: #8d9c9e;
      font-family: 'Poppins', sans-serif;
      color: white;
      overflow-x: hidden;
    }

    /* === Pantalla de Bloqueo === */
    #lock-screen {
      position: fixed;
      inset: 0;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      z-index: 10000;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      text-align: center;
      padding: 20px;
    }

    .lock-container {
      background: rgba(255, 255, 255, 0.2);
      backdrop-filter: blur(12px);
      border-radius: 20px;
      border: 1px solid rgba(255, 255, 255, 0.3);
      padding: 30px;
      width: 90%;
      max-width: 480px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
      position: relative;
      color: white;
    }

    .lock-close {
      position: absolute;
      top: 15px;
      right: 15px;
      font-size: 1.8rem;
      color: #fff;
      cursor: pointer;
      background: none;
      border: none;
      opacity: 0.9;
    }

    .lock-close:hover {
      opacity: 1;
      transform: scale(1.2);
      transition: 0.3s ease;
    }

    .lock-title {
      font-family: 'Dancing Script', cursive;
      font-size: 2.4rem;
      margin-bottom: 15px;
      color: #fff;
      text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
    }

    .lock-text {
      font-size: 1.1rem;
      line-height: 1.7;
      margin-bottom: 25px;
      opacity: 0.95;
    }

    .btn {
      display: inline-block;
      padding: 14px 26px;
      margin: 10px 5px;
      background: #ffffff;
      color: #e91e63;
      font-weight: 600;
      border: none;
      border-radius: 50px;
      font-size: 1.1rem;
      cursor: pointer;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
      transition: all 0.3s ease;
    }

    .btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
    }

    .btn-whatsapp {
      background: #25D366;
      color: white;
    }

    .credits-small {
      font-size: 0.9rem;
      margin-top: 25px;
      opacity: 0.85;
    }

    /* === Corazones flotando === */
    .floating-heart {
      position: absolute;
      font-size: 1.8rem;
      color: rgba(255, 255, 255, 0.6);
      pointer-events: none;
      animation: float 6s infinite ease-in-out;
    }

    @keyframes float {
      0% { transform: translateY(0) rotate(0deg); opacity: 0.6; }
      50% { transform: translateY(-25px) rotate(15deg); opacity: 1; }
      100% { transform: translateY(0) rotate(0deg); opacity: 0.6; }
    }

    /* === Carta de Amor (fuente más gruesa) === */
    .love-letter {
      position: relative;
      width: 90%;
      max-width: 800px;
      margin: 30px auto 20px auto;
      padding: 30px;
      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(10px);
      border-radius: 16px;
      border: 1px solid rgba(255, 255, 255, 0.2);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
      color: #fff;
      line-height: 1.8;
      z-index: 1;
    }

    .love-letter h2 {
      font-family: 'Dancing Script', cursive;
      font-size: 2.6rem;
      text-align: center;
      color: #ff9aa2;
      margin-bottom: 18px;
      letter-spacing: 1px;
      font-weight: 700;
    }

    .love-letter p {
      font-size: 1.25rem;
      font-weight: 500;
      text-align: center;
      margin-bottom: 14px;
      opacity: 0.98;
    }

    .love-letter .signature {
      font-family: 'Dancing Script', cursive;
      font-size: 2rem;
      text-align: right;
      color: #ffb7b7;
      margin-top: 25px;
    }

    /* === Canvas 3D === */
    .webgl {
      position: fixed;
      top: 0;
      left: 0;
      outline: none;
      z-index: -1;
    }

    /* === Créditos inferiores === */
    footer.credits {
      position: fixed;
      bottom: 15px;
      left: 50%;
      transform: translateX(-50%);
      width: auto;
      padding: 10px 18px;
      background: rgba(0, 0, 0, 0.6);
      backdrop-filter: blur(6px);
      border-radius: 10px;
      border: 1px solid rgba(255, 255, 255, 0.25);
      text-align: center;
      font-size: 0.95rem;
      color: #ffd1dc;
      font-family: 'Poppins', sans-serif;
      z-index: 100;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
    }

    footer.credits a {
      color: #ff9aa2;
      text-decoration: none;
      font-weight: 600;
    }

    footer.credits a:hover {
      text-decoration: underline;
    }

    /* === Explosión de corazones === */
    .heart-particle {
      position: absolute;
      font-size: 1.4rem;
      color: #ff69b4;
      pointer-events: none;
      z-index: 9999;
      user-select: none;
      opacity: 0;
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
      float animatedTime = time - delay;
      animatedTime = mod(animatedTime, colorSpeed);
      float mixFactor = animatedTime / colorSpeed;
      vec3 mixedColor = mix(baseColor, finalColor, mixFactor);
      gl_FragColor = vec4(mixedColor, 1.0);
    }
  </script>
</head>
<body>

  <!-- 🛑 PANTALLA DE BLOQUEO -->
  <div id="lock-screen">
    <div class="lock-container animate__animated animate__fadeInUp">
      <button class="lock-close" onclick="showWarning()">×</button>

      <h2 class="lock-title">🔐 Acceso Restringido</h2>
      <p class="lock-text">
        Para ver esta sorpresa especial, debes seguir a <strong>BerMatMods</strong> en TikTok ❤️
      </p>

      <a href="https://www.tiktok.com/@bermat_mods?_t=ZS-8zXCBnq2dlv&_r=1" target="_blank" class="btn" onclick="followAndUnlock(event)">
        Seguir ahora
      </a>

      <a href="https://wa.me/51930569195" target="_blank" class="btn btn-whatsapp">
        Personalización por WhatsApp 💬
      </a>

      <p class="credits-small">
        by AnthZz Berrocal | BerMatMods
      </p>
    </div>

    <!-- Corazones flotando -->
    <script>
      for (let i = 0; i < 15; i++) {
        const heart = document.createElement('div');
        heart.className = 'floating-heart';
        heart.innerHTML = '❤️';
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.top = Math.random() * 100 + 'vh';
        heart.style.animationDelay = Math.random() * 5 + 's';
        heart.style.opacity = Math.random() * 0.5 + 0.5;
        document.getElementById('lock-screen').appendChild(heart);
      }
    </script>
  </div>

  <!-- 💌 CARTA DE AMOR -->
  <div class="love-letter">
    <h2>Para Ti, Con Amor</h2>
    <p>Cada estrella en este universo, cada parpadeo de luz, cada susurro del viento... todo me recuerda a ti.</p>
    <p>Este pequeño mundo fue creado solo para ti, con cada detalle pensado en tu sonrisa, en tu mirada, en tu corazón.</p>
    <p>No es magia, es amor. El mismo que siento cada vez que pienso en ti.</p>
    <p>Gracias por ser mi inspiración, mi paz, mi razón para crear algo hermoso.</p>
    <div class="signature">— Siempre tuyo 💖</div>
  </div>

  <!-- CANVAS 3D -->
  <canvas class="webgl"></canvas>

  <!-- CRÉDITOS -->
  <footer class="credits">
    by AnthZz Berrocal | <a href="https://bermatmods.com" target="_blank">BerMatMods</a>
  </footer>

  <!-- SCRIPT PRINCIPAL -->
  <script type="module">
    // Verificar si ya se "siguió" al cargar
    window.addEventListener('load', () => {
      if (localStorage.getItem('followedBermatMods') === 'true') {
        document.getElementById('lock-screen').remove();
        initThreeJS();
      }
    });

    // Mostrar advertencia si cierra
    function showWarning() {
      alert("⚠️ El sistema ha detectado que no sigues a BerMatMods.\nPor favor, sigue la cuenta para continuar.");
      setTimeout(() => {
        window.open("https://www.tiktok.com/@bermat_mods?_t=ZS-8zXCBnq2dlv&_r=1", "_blank");
      }, 1000);
    }

    // Marcar como seguido y abrir TikTok
    function followAndUnlock(e) {
      e.preventDefault();
      localStorage.setItem('followedBermatMods', 'true'); // Marcar como seguido
      window.open("https://www.tiktok.com/@bermat_mods?_t=ZS-8zXCBnq2dlv&_r=1", "_blank");
      setTimeout(() => {
        document.getElementById('lock-screen').remove();
        initThreeJS();
      }, 500);
    }

    // Explosión de corazones al hacer clic
    document.body.addEventListener('click', (e) => {
      if (document.getElementById('lock-screen')) return;
      createHeartExplosion(e.clientX, e.clientY);
    });

    function createHeartExplosion(x, y) {
      for (let i = 0; i < 20; i++) {
        const heart = document.createElement('div');
        heart.className = 'heart-particle';
        heart.textContent = '❤️';
        document.body.appendChild(heart);

        const angle = (Math.PI * 2 * i) / 20;
        const distance = 100 + Math.random() * 60;
        const targetX = x + Math.cos(angle) * distance;
        const targetY = y + Math.sin(angle) * distance;

        heart.style.left = `${x}px`;
        heart.style.top = `${y}px`;

        setTimeout(() => {
          heart.style.transition = 'all 1.2s cubic-bezier(0.17, 0.67, 0.83, 0.67)';
          heart.style.opacity = '1';
          heart.style.transform = `translate(${targetX - x}px, ${targetY - y}px) scale(2) rotate(${Math.random() * 360}deg)`;
        }, 10);

        setTimeout(() => heart.remove(), 1200);
      }
    }

    // Inicializar Three.js
    async function initThreeJS() {
      import * as THREE from "https://esm.sh/three@0.151.3";
      import { OrbitControls } from "https://esm.sh/three@0.151.3/addons/controls/OrbitControls.js";
      import { OutlineEffect } from "https://esm.sh/three@0.151.3/addons/effects/OutlineEffect.js";
      import { GLTFLoader } from "https://esm.sh/three@0.151.3/examples/jsm/loaders/GLTFLoader.js";

      // === Copia tu código Three.js desde aquí (igual que antes) ===
      // (Lo mantengo resumido por longitud, pero es idéntico al anterior)

      const _VS = `
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
      `;

      const _FS = `
        uniform sampler2D diffuseTexture;
        varying vec4 vColor;
        varying vec2 vAngle;

        void main() {
          vec2 coords = (gl_PointCoord - 0.5) * mat2(vAngle.x, vAngle.y, -vAngle.y, vAngle.x) + 0.5;
          gl_FragColor = texture2D(diffuseTexture, coords) * vColor;
        }
      `;

      function getLinearSpline(lerp) {
        const points = [];
        function addPoint(t, d) { points.push([t, d]); }
        function getValueAt(t) {
          let p1 = 0;
          for (let i = 0; i < points.length; i++) {
            if (points[i][0] >= t) break;
            p1 = i;
          }
          const p2 = Math.min(points.length - 1, p1 + 1);
          if (p1 === p2) return points[p1][1];
          return lerp((t - points[p1][0]) / (points[p2][0] - points[p1][0]), points[p1][1], points[p2][1]);
        }
        return { addPoint, getValueAt };
      }

      function getParticleSystem(params) {
        const { camera, emitter, parent, rate, texture } = params;
        const uniforms = {
          diffuseTexture: { value: new THREE.TextureLoader().load(texture) },
          pointMultiplier: { value: window.innerHeight / (2.0 * Math.tan(30.0 * Math.PI / 180.0)) }
        };
        const material = new THREE.ShaderMaterial({
          uniforms: uniforms,
          vertexShader: _VS,
          fragmentShader: _FS,
          blending: THREE.AdditiveBlending,
          depthTest: true,
          depthWrite: false,
          transparent: true,
          vertexColors: true
        });

        const geometry = new THREE.BufferGeometry();
        geometry.setAttribute('position', new THREE.Float32BufferAttribute([], 3));
        geometry.setAttribute('size', new THREE.Float32BufferAttribute([], 1));
        geometry.setAttribute('aColor', new THREE.Float32BufferAttribute([], 4));
        geometry.setAttribute('angle', new THREE.Float32BufferAttribute([], 1));

        const points = new THREE.Points(geometry, material);
        parent.add(points);
        let particles = [];

        const alphaSpline = getLinearSpline((t, a, b) => a + t * (b - a));
        alphaSpline.addPoint(0.0, 0.0);
        alphaSpline.addPoint(0.6, 1.0);
        alphaSpline.addPoint(1.0, 0.0);

        const colorSpline = getLinearSpline((t, a, b) => a.clone().lerp(b, t));
        colorSpline.addPoint(0.0, new THREE.Color(0xFFFFFF));
        colorSpline.addPoint(1.0, new THREE.Color(0xff8080));

        const sizeSpline = getLinearSpline((t, a, b) => a + t * (b - a));
        sizeSpline.addPoint(0.0, 0.0);
        sizeSpline.addPoint(1.0, 1.0);

        const radius = 0.5;
        const maxLife = 1.5;
        const maxSize = 3.0;
        let accumulator = 0.0;

        function addParticles(timeElapsed) {
          accumulator += timeElapsed;
          const n = Math.floor(accumulator * rate);
          accumulator -= n / rate;
          for (let i = 0; i < n; i++) {
            const life = (Math.random() * 0.75 + 0.25) * maxLife;
            particles.push({
              position: new THREE.Vector3(
                (Math.random() * 1.5 - 1) * radius,
                (Math.random() * 0.125 - 1) * radius,
                (Math.random() * 1.5 - 1) * radius
              ).add(emitter.position),
              size: (Math.random() * 0.5 + 0.5) * maxSize,
              colour: new THREE.Color(),
              alpha: 1.0,
              life: life,
              maxLife: life,
              rotation: Math.random() * 2.0 * Math.PI,
              rotationRate: Math.random() * 0.01 - 0.005,
              velocity: new THREE.Vector3(0, 1.5, 0)
            });
          }
        }

        function updateGeometry() {
          const positions = [], sizes = [], colours = [], angles = [];
          for (const p of particles) {
            positions.push(p.position.x, p.position.y, p.position.z);
            colours.push(p.colour.r, p.colour.g, p.colour.b, p.alpha);
            sizes.push(p.currentSize);
            angles.push(p.rotation);
          }
          geometry.setAttribute('position', new THREE.Float32BufferAttribute(positions, 3));
          geometry.setAttribute('size', new THREE.Float32BufferAttribute(sizes, 1));
          geometry.setAttribute('aColor', new THREE.Float32BufferAttribute(colours, 4));
          geometry.setAttribute('angle', new THREE.Float32BufferAttribute(angles, 1));
          ['position', 'size', 'aColor', 'angle'].forEach(attr => {
            geometry.attributes[attr].needsUpdate = true;
          });
        }

        function updateParticles(timeElapsed) {
          for (const p of particles) p.life -= timeElapsed;
          particles = particles.filter(p => p.life > 0);
          for (const p of particles) {
            const t = 1.0 - p.life / p.maxLife;
            p.rotation += p.rotationRate;
            p.alpha = alphaSpline.getValueAt(t);
            p.currentSize = p.size * sizeSpline.getValueAt(t);
            p.colour.copy(colorSpline.getValueAt(t));
            p.position.add(p.velocity.clone().multiplyScalar(timeElapsed));
            const drag = p.velocity.clone().multiplyScalar(timeElapsed * 0.1);
            ['x', 'y', 'z'].forEach(axis => {
              const d = drag[axis];
              const v = p.velocity[axis];
              drag[axis] = Math.sign(v) * Math.min(Math.abs(d), Math.abs(v));
            });
            p.velocity.sub(drag);
          }
          particles.sort((a, b) => camera.position.distanceTo(b.position) - camera.position.distanceTo(a.position));
        }

        return {
          update: (timeElapsed) => {
            addParticles(timeElapsed);
            updateParticles(timeElapsed);
            updateGeometry();
          }
        };
      }

      const canvas = document.querySelector('canvas.webgl');
      const scene = new THREE.Scene();
      const gltfLoader = new GLTFLoader();
      const textureLoader = new THREE.TextureLoader();
      const sizes = {
        width: window.innerWidth,
        height: window.innerHeight
      };

      const camera = new THREE.PerspectiveCamera(10, sizes.width / sizes.height, 0.1, 1000);
      const controls = new OrbitControls(camera, canvas);
      const minPan = new THREE.Vector3(-5, -2, -5);
      const maxPan = new THREE.Vector3(5, 2, 5);
      const clock = new THREE.Clock();
      let mixer;

      const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
      const effect = new OutlineEffect(renderer, {
        defaultThickness: 0.0014,
        defaultColor: [0.125, 0.125, 0.125],
        defaultAlpha: 1,
        defaultVisible: true
      });
      renderer.setSize(sizes.width, sizes.height);
      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

      // Luces
      const ambientLight = new THREE.AmbientLight("#ffffff", 0.9);
      scene.add(ambientLight);
      const directionalLight = new THREE.DirectionalLight('#ffffff');
      directionalLight.position.set(-2, 5, 0);
      directionalLight.intensity = 0.35;
      scene.add(directionalLight);

      // Controles
      controls.enableDamping = true;
      controls.enableZoom = true;
      controls.enablePan = true;
      controls.minPolarAngle = Math.PI / 5;
      controls.maxPolarAngle = Math.PI / 2;
      controls.minDistance = 20;
      controls.maxDistance = 47;

      // Cámara
      camera.position.set(35, 8, 36);
      scene.add(camera);

      // Materiales
      const bakedTexture = textureLoader.load('https://rawcdn.githack.com/ricardoolivaalonso/threejs-journey01/e3cfc35a8270972a21435ad885da2bab54ec2d11/baked.jpg');
      bakedTexture.flipY = false;
      const bakedMaterial = new THREE.MeshStandardMaterial({ map: bakedTexture, side: THREE.DoubleSide, roughness: 0.5 });

      const snowMaterial = new THREE.MeshPhysicalMaterial({ color: 0xeeeeee, roughness: 0.6, metalness: 0.1, reflectivity: 0.75 });
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
      fireMaterial.userData.outlineParameters = { thickness: 0 };

      // Cargar modelos
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

      // Fuego (partículas)
      const cube = new THREE.Mesh(
        new THREE.BoxGeometry(1, 0.01, 0.5),
        new THREE.MeshStandardMaterial({ color: 0xffffff })
      );
      cube.position.set(0.1, -2.2, -1.6);
      scene.add(cube);

      const fireEffect = getParticleSystem({
        camera,
        emitter: cube,
        parent: scene,
        rate: 200,
        texture: 'https://rawcdn.githack.com/ricardoolivaalonso/threejs-journey01/e3cfc35a8270972a21435ad885da2bab54ec2d11/fire.png'
      });

      // Loop
      const tick = () => {
        requestAnimationFrame(tick);
        const delta = clock.getDelta();
        if (mixer) mixer.update(delta);
        neonMaterial.uniforms.time.value += 0.075;
        neonMaterial2.uniforms.time.value += 0.09;
        fireEffect.update(0.016);
        controls.update();
        controls.target.clamp(minPan, maxPan);
        effect.render(scene, camera);
      };

      window.addEventListener('resize', () => {
        sizes.width = window.innerWidth;
        sizes.height = window.innerHeight;
        camera.aspect = sizes.width / sizes.height;
        camera.updateProjectionMatrix();
        renderer.setSize(sizes.width, sizes.height);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      });

      tick();
    }
  </script>
</body>
</html>
