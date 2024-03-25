<script>
	import * as THREE from 'three';
	import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
	import Stats from 'three/examples/jsm/libs/stats.module'

	// Create the main scene
	const scene = new THREE.Scene();
	const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

	// Create the renderer
	const renderer = new THREE.WebGLRenderer();
	renderer.setSize( window.innerWidth, window.innerHeight );
	document.body.appendChild( renderer.domElement );

	// Add the stats visor
	const stats = new Stats();
	document.body.appendChild(stats.dom)

	// Add Controls to navigate into main scene
	const controls = new OrbitControls(camera, renderer.domElement);

	// Add Grid helper
	const grid = new THREE.GridHelper(1000, 1000);

	// Create a cube
	const geometry = new THREE.BoxGeometry( 1, 1, 1 );
	const material = new THREE.MeshBasicMaterial( { color: 0x00ff00, wireframe: true } );
	const cube = new THREE.Mesh( geometry, material );

	// Add elements to scene
	scene.add( cube );
	scene.add( grid );

	// Set camera position
	camera.position.set(1, 3, 4);

	// Main function to animate all frames
	function animate() {
		requestAnimationFrame( animate );

		cube.rotation.x += 0.01;
		cube.rotation.y += 0.01;

		renderer.render( scene, camera );
		stats.update();	
	}

	window.addEventListener('resize', function () {
		camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
	})

	// Calling the main function
	animate();
</script>