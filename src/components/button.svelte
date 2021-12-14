<script>
    export let call=" ";
    export let title;
    export let type;

    import CursorType from "../stores/cursor.js";

    const changeCursor = (type = "default") => {
        CursorType.update(() => type)
    }

</script>
<style>
    button{
        background-color: var(--color_primary);
        border: none;
        border-radius: var(--radius_curvy);
        color: white;
        cursor: none;
        font-size: 1rem;
        height: 3rem;
        width: 9rem;
    }
    .contact{
        box-shadow: 0px 4px 14px var(--color_primary_fade);
        transition: transform 0.2s ease-out;
    }
</style>
<button class="{type}" title={title} on:mouseenter={() => changeCursor("large")} on:mouseleave={changeCursor}>{call}</button>