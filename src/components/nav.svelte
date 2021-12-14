<script>
    import Button from './button.svelte';
    import Link from './link.svelte';
</script>
<style>
    #logo, ul, li, .contact{
        display: inline-block;
    }
    nav{
        background: transparent;
        display: grid;
        grid-template-columns: 1fr 3fr 1fr;
        height: 3rem;
        margin: 0;
        padding: 1rem var(--padding_section);
    }
    #logo img{
        margin: 1rem 0 0 0;
    }
    ul{
        margin: 0;
        padding: 0;
        text-align: center;
    }
    li{
        font-size: 1.1rem;
        margin: 1rem 3rem 0 3rem;
    }
    #logo, .contact{
        display: grid;
        justify-content: center;
    }
</style>
<nav>
    <div id="logo">
        <img src="#" title="askdamaris.com's logo" alt="askdamaris.com's logo"/>
    </div>
    <ul>
        <li><Link link="#about" linkText="about" /></li>
        <li><Link link="#services" linkText="Services" /></li>
        <li><Link link="#videos" linkText="Videos" /></li>
    </ul>
    <div class="contact">
        <Button type="contact" title="ask damaris" call="Contact Us" />
    </div>
</nav>