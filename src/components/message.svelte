<script>
    export let message;
    export let shadowVal = 0;
    export let clone = false;
    export let icon;
    export let move;

    import Link from "./link.svelte";

</script>
<style>
    .message{
        border-radius: var(--radius_boxy);
        box-shadow: var(--shadow_no_spread);
        cursor: none;
        display: grid;
        grid-template-columns: 1fr 11fr;
        height: 6rem;
        margin: 0 auto 1.5rem auto;
        opacity: 0.75;
        padding: 1rem;
        transition: box-shadow 0.2s ease-out, opacity 0.2s ease-out;
        width: 100%;
    }
    .message:hover{
        box-shadow: var(--shadow);
        opacity: 1;
    }
    .icon{
        border-radius: var(--radius_boxy);
        box-shadow: var(--shadow_no_spread);
        display: inline-block;
        height: 4rem;
        width: 4rem;
    }
    p{
        display: inline-block;
        font-size: 1.5rem;
        font-weight: bold;
        margin: 0;
        text-align: center;
    }
</style>
<div class="message" 
     style="transform: translateY({(clone ? -7.5 : 0 ) + move}rem);opacity:{shadowVal > 0 ? shadowVal + 0.5:''};">
    <div class="icon">
        <img src="{icon}" alt="icon" />
    </div>
    <p>
        <Link linkText="{message}" />
    </p>
</div>