<script>
    import VideoCard from "./video_card.svelte";

    $:youtubeVids = [{
        snippet:{
            title: "error",
            thumbnails:{
                medium: {
                    url: "dummy.png"
                }
            }
        },
    },
    {snippet:{
            title: "error",
            thumbnails:{
                medium: {
                    url: "dummy.png"
                }
            }
    }}];

    $:distance = 0;
    let scrollWidth;
    let cardWidth;

    const walk = () => scrollWidth > cardWidth ? cardWidth * 0.5 : scrollWidth * 0.5;

    fetch("https://youtube.googleapis.com/youtube/v3/search?part=snippet&channelId=UC4at4KAGTVXStGhsAxK_Ypg&maxResults=30&order=date&key=AIzaSyCE43PoxOncz5xC5TkrVsuNbKvpk9hFOyQ")
    .then(result => result.json())
    .then(
        youtubeData => {
            if(youtubeData.hasOwnProperty("error")) return;
            youtubeVids = youtubeData.items;
        }
    )
    .catch( error => {
        console.log(error) 
    }
    );
    const moveRight = () =>{
        if(distance < 0){
            distance += walk();
        }
        return;
    }
    const moveLeft = () =>{
        if(distance > (youtubeVids.length - 1) * - cardWidth){
            distance -= walk();
        }
        return;
    }
</script>
<style>
    h1{
        text-align: center;
    }
    .videos{
        padding: 0 var(--padding_section);
    }
    .scroll_container{
        position: relative;
        margin: 0;
        padding: 0;
        width: 100%;
    }
    .scroll{
        direction: inherit;
        margin: 0;
        padding: 2rem 0;
        position: relative;
        overflow: hidden;
        white-space: nowrap;
        width: 100%;
    }
    .scroll_edge{
        background: red;
        display: inline-block;
        height: 100%;
        position: absolute;
        top: 0;
        width: 4rem;
        z-index: 2;
    }
    .scroll_edge.right{
        background: linear-gradient(to left, rgba(255, 255, 255, 1) 0%, rgba(255, 255, 255,0) 100%);
        right: 0;
    }
    .scroll_edge.left{
        background: linear-gradient(to right, rgba(255, 255, 255, 1) 0%, rgba(255, 255, 255,0) 100%);
        left: 0;
    }

</style>

<div id="videos" class="videos">
    <h1>Videos</h1>
    <div class="scroll_container" bind:clientWidth={scrollWidth}>
        <div class="scroll_edge left" on:click={moveRight}></div>
        <div class="scroll">
            {#each youtubeVids as youtubeVid}
                <VideoCard thumbnail="{youtubeVid.snippet.thumbnails.medium.url}" imgAlt="{youtubeVid.snippet.title}" distance={distance} bind:cardWidth={cardWidth}/>
            {/each}
        </div>
        <div class="scroll_edge right" on:click={moveLeft}></div>
    </div>
</div>
