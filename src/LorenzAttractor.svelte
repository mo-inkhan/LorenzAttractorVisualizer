<script>
    import P5 from "p5-svelte";
    let enableCamera = false;

    const sketch = (p) => {
        let x = 0.01;
        let y = 0;
        let z = 0;
        let a = 10;
        let b = 28;
        let c = 8.0 / 3.0;
        let points = [];

        p.setup = () => {
            p.createCanvas(800, 600, p.WEBGL);
            p.colorMode(p.HSB);
            // p.frameRate(1200);
        };

        p.draw = () => {
            let dt = 0.01;
            let dx = a * (y - x) * dt;
            let dy = (x * (b - z) - y) * dt;
            let dz = (x * y - c * z) * dt;
            x = x + dx;
            y = y + dy;
            z = z + dz;

            points.push(new p.Vector(x, y, z));

            p.background(0);
            p.translate(0, 0, -80);
            let camX = p.map(p.mouseX, 0, p.width, -200, 200);
            let camY = p.map(p.mouseY, 0, p.height, -200, 200);
            enableCamera &&
                p.camera(
                    camX,
                    camY,
                    p.height / 2.0 / p.tan((p.PI * 30.0) / 180.0),
                    0,
                    0,
                    0,
                    0,
                    1,
                    0
                );
            p.scale(5);
            p.stroke(255);
            p.noFill();

            let hu = 0;
            p.beginShape();
            for (let v of points) {
                p.stroke(hu, 255, 255);
                p.vertex(v.x, v.y, v.z);
                hu += 0.1;
                if (hu > 255) {
                    hu = 0;
                }
            }
            p.endShape();
        };
    };
</script>

<div class="container-action" on:click={() => (enableCamera = !enableCamera)}>
    {enableCamera ? "Disable" : "Enable"} mouse movement
</div>
<div class="container">
    <P5 {sketch} />
</div>

<style>
    .container-action {
        color: #ffffff;
        text-align: center;
    }
    .container {
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>
