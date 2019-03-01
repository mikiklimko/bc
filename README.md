# bc
# bc
<!DOCTYPE html>
<html>

<head>
    <title>skuska</title>
    <script scr="js/dat.gui.min.js"> </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r79/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/dat-gui/0.7.2/dat.gui.js"></script>
    <script scr="js/three.min.js"> </script>
    
    <style>
        body {
            margin: 0;
        }

        canvas {
            width: 100%;
            height: 100%;
        }
    </style>
</head>

<body>
<script>
        var scene, camera, renderer;

        var gui, cube, xro, yro, zro;

        init();
        animate();


        function init() {

            scene = new THREE.Scene();

            camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            renderer = new THREE.WebGLRenderer();
            renderer.setClearColor(0x0f0f0f, 1);
            renderer.setSize(window.innerWidth, window.innerHeight);
            document.body.appendChild(renderer.domElement);

            var geometry = new THREE.BoxGeometry(1, 1, 1);
            var material = new THREE.MeshBasicMaterial({ color: 0x0000ff });
            cube = new THREE.Mesh(geometry, material);
            scene.add(cube);

            


            camera.position.x = 2;
            camera.position.y = 1, 2;
            camera.position.z = 4;
            dispalygui();

        }


        function spin(varname, xaxis, yaxis, zaxis) {

            var speed = 0.1;

            if (varname == true) {

                if (xaxis == true) { cube.rotation.x += speed; }
                else if (yaxis == true) { cube.rotation.y += speed; }
                else cube.rotation.z += speed;
            }
        }
        function dispalygui() {



            var gui = new dat.GUI();
            var jar;
            var speed = 0.1;
            parameters = {
                a: "Cube",
                b: "",
                c: true,
                d: "#0000ff",
                e: 1, f: 1, g: 1,
                h: 1, i: 1, j: 1,
                k: 1, l: 1, m: 1,
                x: false, y: false, z: false,
                n: "",
                o: "",



            }

            gui.add(parameters, 'a').name('Name');
            gui.add(parameters, 'b', ["Cube", "Sphere", "Prism"]).name('Geometry');

            //5:25
            var model = gui.add(parameters, "c").name("Show Model");
            var color = gui.addColor(parameters, 'd').name('Color');

            model.onChange(function (jar) { cube.visible = jar; });
            color.onChange(function (jar) { cube.material.color.setHex(jar.replace("#", "0x")); });

            var dimen = gui.addFolder('Dimension');
            var xdimen = dimen.add(parameters, 'e').min(1).max(20).step(speed).name('X-Axis');
            var ydimen = dimen.add(parameters, 'f').min(1).max(20).step(speed).name('Y-Axis');
            var zdimen = dimen.add(parameters, 'g').min(1).max(20).step(speed).name('Z-Axis');

            xdimen.onChange(function (jar) { cube.scale.x = jar; });
            ydimen.onChange(function (jar) { cube.scale.y = jar; });
            zdimen.onChange(function (jar) { cube.scale.z = jar; });



            var posit = gui.addFolder('Position');
            var xspot = posit.add(parameters, 'h').min(-10).max(20).step(speed).name('X-Axis');
            var yspot = posit.add(parameters, 'i').min(-10).max(20).step(speed).name('Y-Axis');
            var zspot = posit.add(parameters, 'j').min(-10).max(20).step(speed).name('Z-Axis');

            xspot.onChange(function (jar) { cube.position.x = jar; });
            yspot.onChange(function (jar) { cube.position.y = jar; });
            zspot.onChange(function (jar) { cube.position.z = jar; });



            var rotat = gui.addFolder('Rotation');
            var xspin = rotat.add(parameters, 'k').min(-10).max(20).step(speed).name('X-Axis');
            var yspin = rotat.add(parameters, 'l').min(-10).max(20).step(speed).name('Y-Axis');
            var zspin = rotat.add(parameters, 'm').min(-10).max(20).step(speed).name('Z-Axis');

            xspin.onChange(function (jar) { cube.rotation.x = jar; });
            yspin.onChange(function (jar) { cube.rotation.y = jar; });
            zspin.onChange(function (jar) { cube.rotation.z = jar; });



            var anim = gui.addFolder('Animation');
            var xanim = anim.add(parameters, 'x').name('X-Axis');
            var yanim = anim.add(parameters, 'y').name('Y-Axis');
            var zanim = anim.add(parameters, 'z').name('Z-Axis');

            xanim.onChange(function (jar) { xro = jar; });
            yanim.onChange(function (jar) { yro = jar; });
            zanim.onChange(function (jar) { zro = jar; });




            gui.add(parameters, 'n', [1, 2, 3, 4, 5]).name('Layer');
            gui.add(parameters, 'o', ["Save", "Load", "Reset"]).name('Option');


            //gui.close();
            gui.open();


        }
        function animate() {
            spin(xro, true, false, false);
            spin(yro, false, true, false);
            spin(zro, false, false, true);

            requestAnimationFrame(animate);
            render();

        }

        function render() {
            renderer.clear();
            renderer.render(scene, camera);
        }

    </script>

</body>

</html>