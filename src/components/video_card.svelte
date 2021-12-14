<script>
    export let thumbnail;
    export let imgAlt;
    export let distance;
    export let cardWidth;
</script>
<style>
.video_card{
    border: none;
    border-radius: var(--radius_curvy);
    box-shadow: var(--shadow);
    display: inline-block;
    height: 500px;
    margin: 0 1rem;
    position: relative;
    width: 400px;
}
.video_card:hover{
    box-shadow: var(--shadow_no_spread);
}
.video_thumbnail{
    
    border-radius: var(--radius_curvy) var(--radius_curvy) 0 0;
    box-sizing: border-box;
    height: 60%;
    object-fit: cover;
    overflow: hidden;
    position: relative;
}
.video_thumbnail img, .overlay{
    height: 100%;
    object-fit: cover;
    position: absolute;
    width: 100%;
}
.overlay{
    background: var(--color_primary_shade);
    opacity: 0.2;
    transition: opacity 0.5s ease-out;
    z-index: 2;
}
.overlay:hover{
    opacity: 0;
}
</style>
<div class="video_card" style="transform: translateX({distance}px);" bind:clientWidth={cardWidth}>
    <div class="video_thumbnail"> 
        <img src="{thumbnail}" alt="{imgAlt}" />
        <div class="overlay"></div>
    </div>
    <div class="video_info">

    </div>
</div>