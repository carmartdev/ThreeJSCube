# Accessible 3D Cube using Three.js

This is an example of creating an accessible web page where a 3D cube with applied texture is rendered using Three.js. The cube spins slowly in both x and y dimensions.

The HTML portion contains an instructional div element and a container div, where the 3D object will be rendered.

Aria roles and labels are included to make the page more accessible.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>3D Cube with Texture</title>
  <style>
    body { margin: 0; }
    #container { display: block; }
    #instructions {
      position: absolute;
      top: 10px; left: 10px;
      padding: 5px;
      font-size: 18px;
      background: white;
    }
  </style>
  <script src="https://threejs.org/build/three.js"></script>
</head>
<body>
  <div role="main">
    <div id="instructions" aria-live="polite">
      Use your mouse to rotate, zoom, and pan the scene.
    </div>
    <div id="container" role="region" aria-label="3D Scene"></div>
  </div>

  <script>
    // Basic setup for the Three.js scene
    var scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.getElementById('container').appendChild(renderer.domElement);

    // Load the texture
    var texture = new THREE.TextureLoader().load('https://github.com/carmartdev/Display-Key-Presses/raw/main/images/example1.png');
    var geometry = new THREE.BoxGeometry(1, 1, 1);
    var material = new THREE.MeshBasicMaterial({ map: texture });
    var cube = new THREE.Mesh(geometry, material);

    // Add the cube to the scene and position the camera
    scene.add(cube);
    camera.position.z = 5;

    // Animation function
    function animate(){
      requestAnimationFrame(animate);
      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;
      renderer.render(scene, camera);
    }

    // Start the animation
    animate();
  </script>
</body>
</html>
