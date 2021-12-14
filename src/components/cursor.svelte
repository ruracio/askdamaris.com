<script>
    import CursorType from '../stores/cursor.js'
    $: cursor = {
        top: "0px",
        left: "0px"
    }

    const followCursor = (event) =>{
        cursor.left = event.pageX + "px";
        cursor.top = event.pageY + "px";
    };
</script>
<style>
    .cursor{
        background-color: var(--color_secondary);
        border-radius: 50%;
        height: 20px;
        mix-blend-mode: multiply;
        pointer-events: none;
        position: absolute;
        transform: translate(-50%, -50%);
        transition: transform 0.1s ease-out;
        width: 20px;
        z-index: 10;
    }
    .large{
        transform: scale(3);
    }
</style>
<svelte:body on:mousemove={followCursor}/>
<div class="cursor {$CursorType}" style="top:{cursor.top};left:{cursor.left};"></div>