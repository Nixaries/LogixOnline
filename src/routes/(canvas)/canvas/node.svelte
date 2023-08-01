<script lang="ts">
    import {onMount} from 'svelte';

    let x = 10;
    let y = 10;

    export let offsetX: number;
    export let offsetY: number; 

    let dragging = false;

    onMount(() => {
    function onMouseMove(e:MouseEvent) {
        if(dragging) {
            x += e.movementX;
            y += e.movementY;
        }
    }

    document.addEventListener('mousemove', onMouseMove);

    document.addEventListener('mouseup', (e:MouseEvent) => {
        dragging = false;
    });
    })


    function onClick(e:MouseEvent) {
        dragging = true;
    }

</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div class="node" style="top: {y + offsetY}px; left: {x + offsetX}px;" on:mousedown={onClick}>

</div>

<style>
.node {
    position: absolute;
    height:50px;
    width:50px;
    background-color: red;
}
</style>