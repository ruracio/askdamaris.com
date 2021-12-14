<script>
    import Message from './message.svelte';
    import {tweened} from 'svelte/motion';

    $:messages = [
        {
            title: 'one on one consultation',
            icon: '#',
            position: 1
        },
        {
            title: 'training and workshop',
            icon: '#',
            position: 2
        },
        {
            title: 'business process outsourcing',
            icon: '#',
            position: 3
        }
    ];

    $:clone = messages[messages.length - 1];
    $:move = -7.5;
    $:shadowVal = 2;

    const tweenedMove = tweened(0);
    const tweenedShadow = tweened(0);

    $:tweenedMove.set(move);
    $:tweenedShadow.set(shadowVal);

    let sortByPosition = (msgA, msgB) =>  msgA.position - msgB.position;
    let resetMessages = () => {
        messages.map(msg => {
            msg.position == messages.length ? msg.position = 1 : msg.position += 1;
        });
        clone = messages.filter(msg => msg.position == messages.length)[0];
        messages = messages.sort(sortByPosition);
        move = -7.5;
        shadowVal = 2;
    }
    let trickle = () => {
        move += 7.5;
        shadowVal = 0;
        setTimeout(resetMessages, 1000);
    }
    let startTrickle = () => {
        setInterval(trickle, 4000);
    }

</script>
<style>
    .intro{
        display: grid;
        grid-template-columns: 2fr 3fr;
        min-height: calc(100vh - 5rem);
        padding: 20vh var(--padding_section) 0 var(--padding_section);
    }
    p{
        font-size: 1.4rem;
    }
    .messages{
        height: 21rem;
        margin: 0;
        padding: 0;
        position: relative;
        overflow: hidden;
    }
    .messages::before{
        background: linear-gradient(to top, rgba(255, 255, 255, 1) 0%, rgba(255, 255, 255,0) 100%);
        bottom: 0;
        content: '';
        display: inline-block;
        height: 10%;
        left: 0;
        position: absolute;
        width: 100%;
        z-index: 2;
    }
</style>
<svelte:window on:load={startTrickle()} />
<div class="intro">
    <div id="about" class="area_1">
        <div class="intro_text">
            <h1>Learn and grow</h1>
            <p>Ask Damaris is a platform that gives you an opportunity for self actualisation and supports your business operations in maintaining growth and achieving success.</p>
        </div>
        <div  class="messages">
            <Message icon={clone.icon} message={clone.title} move={move < 0 ? move: $tweenedMove}/>
            {#each messages as {title, icon, position}}
                <Message icon={icon} message={title} shadowVal={position==1 ? $tweenedShadow: 0} move={move < 0 ? move: $tweenedMove}/>
            {/each}
        </div>
    </div>
    <div class="area_2">

    </div>
</div>


