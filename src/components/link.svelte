<script>
    export let link;
    export let linkTitle;
    export let linkText;
    import CursorType from '../stores/cursor.js';

    const changeCursor = (type = "default") => {
        CursorType.update(() => type)
    }

</script>
<style>
    a{
        cursor: none;
        text-decoration: none;
    }
</style> 
<a href="{link}" title="{linkTitle}" on:mouseenter={()=>{changeCursor("large")}} on:mouseleave={changeCursor}>{linkText}</a>