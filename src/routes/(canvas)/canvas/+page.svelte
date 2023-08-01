<script lang="ts">
    import {onMount} from 'svelte';
	import Node from "./node.svelte";

    let offsetX = 0;
    let offsetY = 0;

    let panning = false;

    onMount(() => {
        function canvasMouseDown(e:MouseEvent) {
            if(e.button == 2) {
                panning = true;
            }
        }

        function canvasMouseMove(e:MouseEvent) {
            if(panning) {
                offsetX += e.movementX;
                offsetY += e.movementY;
            }
        }

        function canvasMouseUp(e:MouseEvent) {
            panning = false;
        }

        document.addEventListener('mousedown', canvasMouseDown);
        document.addEventListener('mousemove', canvasMouseMove);
        document.addEventListener('mouseup', canvasMouseUp);
    })
</script>

<div class="canvas" on:contextmenu={() => false}>
    <Node offsetX={offsetX} offsetY={offsetY}/> 
    <Node offsetX={offsetX} offsetY={offsetY}/>
</div>

<style>
.canvas {
    width: 100vw;
    height: 100vh;
    position: relative;
}

.node {
    position: absolute;
}
</style>