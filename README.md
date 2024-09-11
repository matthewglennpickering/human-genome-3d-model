
# 3D Human Genome Structure Visualization in JavaScript

This JavaScript program uses the Three.js library to create a 3D model of the human genome structure, with each chromosome represented by an "X"-shaped object, similar to their appearance during cell division.

## Overview

The human genome consists of 23 pairs of chromosomes. This program provides a basic 3D representation of these chromosomes, arranged in pairs to resemble their natural structure. The chromosomes are represented as "X"-shaped objects, and the scene includes lighting and animations for a dynamic visualization.

## Program Structure

The program is structured into several main components:

1. **Scene Setup**: Creates a Three.js scene, camera, and renderer to set up the 3D environment.
2. **Lighting**: Adds ambient and point lights to illuminate the 3D objects.
3. **Chromosome Model**: Defines the geometry and material of the chromosomes, representing them as "X"-shaped objects.
4. **Rendering and Animation**: Renders the scene and includes an animation loop to rotate the chromosomes continuously.

## Detailed Explanation

### Scene Setup

- Creates a Three.js scene using `THREE.Scene()`.
- Defines a camera with a perspective view (`THREE.PerspectiveCamera`), which sets the field of view, aspect ratio, and rendering distance.
- Initializes the renderer (`THREE.WebGLRenderer`) to display the 3D content in the browser.

### Lighting

- **Ambient Light**: Adds a soft white light that illuminates all objects equally (`THREE.AmbientLight`).
- **Point Light**: Adds a more focused light source to create depth and shadow effects (`THREE.PointLight`).

### Chromosome Model

- **Geometry**: Each chromosome is represented by two cylinders (`THREE.CylinderGeometry`) combined at 45-degree angles to form an "X" shape.
- **Material**: Uses `THREE.MeshPhongMaterial` to add realistic shading and color.
- **Chromosome Creation**: Chromosomes are created in pairs with slight positional offsets to represent their natural arrangement.

### Rendering and Animation

- Sets up a continuous rendering loop (`animate` function) to update the scene, providing rotation effects for dynamic visualization.

## How to Use

1. **Download or Copy the Program Code**: Save the code into an HTML file (e.g., `genome3d.html`).
2. **Open the File in a Web Browser**: Use any modern web browser (such as Chrome or Firefox) to open the file and view the 3D model.
3. **Interact with the Model**: Use your mouse or touchpad to interact with the 3D visualization.

## Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Human Genome Structure</title>
    <style>
        body { margin: 0; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        // Scene setup
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer();
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // Lighting
        const ambientLight = new THREE.AmbientLight(0x404040);
        scene.add(ambientLight);

        const pointLight = new THREE.PointLight(0xffffff, 1, 500);
        pointLight.position.set(50, 50, 50);
        scene.add(pointLight);

        // Function to create a chromosome model with "X" shape
        function createChromosome(name, positionX, positionY, scale = 1) {
            // Chromosome structure
            const material = new THREE.MeshPhongMaterial({ color: Math.random() * 0xffffff });

            // Create two cylinders for the "X" shape
            const armLength = 2 * scale;
            const armThickness = 0.3 * scale;
            const cylinderGeometry = new THREE.CylinderGeometry(armThickness, armThickness, armLength, 32);
            
            const arm1 = new THREE.Mesh(cylinderGeometry, material);
            arm1.rotation.z = Math.PI / 4; // 45 degrees to form the "X"

            const arm2 = new THREE.Mesh(cylinderGeometry, material);
            arm2.rotation.z = -Math.PI / 4; // -45 degrees to form the "X"

            // Combine arms to create the chromosome shape
            const chromosome = new THREE.Group();
            chromosome.add(arm1);
            chromosome.add(arm2);
            chromosome.position.set(positionX, positionY, 0);
            chromosome.name = name;
            return chromosome;
        }

        // Create chromosomes in pairs and add them to the scene
        const chromosomeNames = [
            'Chromosome 1', 'Chromosome 2', 'Chromosome 3', 'Chromosome 4', 'Chromosome 5',
            'Chromosome 6', 'Chromosome 7', 'Chromosome 8', 'Chromosome 9', 'Chromosome 10',
            'Chromosome 11', 'Chromosome 12', 'Chromosome 13', 'Chromosome 14', 'Chromosome 15',
            'Chromosome 16', 'Chromosome 17', 'Chromosome 18', 'Chromosome 19', 'Chromosome 20',
            'Chromosome 21', 'Chromosome 22', 'Chromosome X', 'Chromosome Y'
        ];

        const chromosomeModels = chromosomeNames.map((name, index) => {
            const pairOffset = (index % 2 === 0) ? -0.5 : 0.5; // Slight offset to separate pairs
            const positionX = Math.floor(index / 2) - (chromosomeNames.length / 4); // Position in pairs
            const positionY = pairOffset;
            const scale = (index % 2 === 0) ? 1 : 0.8; // Different scale for variety
            const chromosome = createChromosome(name, positionX, positionY, scale);
            scene.add(chromosome);
            return chromosome;
        });

        // Camera position
        camera.position.z = 20;

        // Animation loop
        function animate() {
            requestAnimationFrame(animate);

            // Rotate chromosomes for a dynamic effect
            chromosomeModels.forEach(chromosome => {
                chromosome.rotation.y += 0.01;
                chromosome.rotation.x += 0.01;
            });

            renderer.render(scene, camera);
        }

        animate();
    </script>
</body>
</html>
```

## Output

When you run the program in a web browser, it will display a 3D model of the human genome, with each chromosome represented as an "X"-shaped object rotating in a 3D space.

## Requirements

- A modern web browser with WebGL support.
- Internet access to load the Three.js library from the CDN, or you can download the library and host it locally.

## License

This program is open-source and available under the MIT License.

## Contributions

Contributions and improvements are welcome! Please feel free to fork the repository and submit pull requests.
# human-genome-3d-model
