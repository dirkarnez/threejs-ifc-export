# threejs-ifc-export
!!!!https://threejs.org/docs/index.html#examples/en/utils/BufferGeometryUtils.mergeGeometries
！！！！https://standards.buildingsmart.org/IFC/DEV/IFC4_2/FINAL/HTML/annex/annex-e/brep-model.ifc.htm
https://standards.buildingsmart.org/IFC/DEV/IFC4_2/FINAL/HTML/annex/annex-e/basin-faceted-brep.ifc
https://standards.buildingsmart.org/IFC/DEV/IFC4_2/FINAL/HTML/annex/annex-e/brep-model.htm


```html
<!DOCTYPE html>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r77/three.js"></script>
<!-- OrbitControls.js is not versioned and may stop working with r77 -->
<script src='http://threejs.org/examples/js/controls/OrbitControls.js'></script>

<body style='margin: 0px; background-color: #bbbbbb; overflow: hidden;'>
  <script>
    // init renderer
    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // init scene and camera
    var scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.01, 3000);
    camera.position.z = 5;
    var controls = new THREE.OrbitControls(camera)
   	
    // our code
    var box = new THREE.BoxGeometry(1, 1, 1);
    var sphere = new THREE.SphereGeometry(.65, 32, 32);

    var singleGeometry = new THREE.Geometry();

    var boxMesh = new THREE.Mesh(box);
    var sphereMesh = new THREE.Mesh(sphere);

    boxMesh.updateMatrix(); // as needed
    singleGeometry.merge(boxMesh.geometry, boxMesh.matrix);

    sphereMesh.updateMatrix(); // as needed
    singleGeometry.merge(sphereMesh.geometry, sphereMesh.matrix);

    var material = new THREE.MeshPhongMaterial({color: 0xFF0000});
    var mesh = new THREE.Mesh(singleGeometry, material);
    scene.add(mesh);

    // a light
    var light = new THREE.HemisphereLight(0xfffff0, 0x101020, 1.25);
    light.position.set(0.75, 1, 0.25);
    scene.add(light);
	
    // render
    requestAnimationFrame(function animate(){
	    requestAnimationFrame(animate);
	    renderer.render(scene, camera);		
    })
  </script>
</body>
```
