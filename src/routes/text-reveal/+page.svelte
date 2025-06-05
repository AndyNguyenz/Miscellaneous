<script>
    import gsap from "gsap";
    import ScrollTrigger from "gsap/dist/ScrollTrigger";
    import { onMount } from "svelte";

    let ref1, ref2;

    let text1 = "You’ve probably heard of Lorem Ipsum before – it’s the most-used dummy text excerpt out there. People use it because it has a fairly normal distribution of letters and words (making it look like normal English), but it’s also Latin, which means your average reader won’t get distracted by trying to read it. It’s perfect for showcasing design work as it should look when fleshed out with text, because it allows viewers to focus on the design work itself, instead of the text. It’s also a great way to showcase the functionality of programs like word processors, font types, and more."
    let chars1 = [];

    let text2 = "Maybe you have a custom-styled ordered list you want to show off, or maybe you just want a long chunk of Lorem Ipsum that’s already wrapped in paragraph tags. No matter the need, we’ve put together a number of Lorem Ipsum samples ready to go with HTML tags and formatting in place. All you have to do is click the heading of any section on this page, and that HTML-Ipsum block is copied to your clipboard and ready to be loaded into a website redesign template, brand new design mockup, or any other digital project you might need dummy text for.";
    let chars2 = [];

    onMount(()=>{
        if (typeof window !== "undefined") {
            gsap.registerPlugin(ScrollTrigger);
        }

        [ref1, ref2].forEach(paragraph=>{
            gsap.from(paragraph.querySelectorAll('.char'), {
                scrollTrigger: {
                    trigger: paragraph,
                    start: "top center",
                    toggleActions: 'play none none reverse',
                },
                opacity: 0,
                y: 40,
                stagger: 0.001,
                duration: 0.01,
                ease: 'power2.out'
            })
        })
        
    });

    chars1 = text1.split('');
    chars2 = text2.split('');
</script>

<div class='main'>
    <section style='margin-top: 500px;'>
        <h1>HTML-Ipsum Info 1</h1>
        <p class='animated-text' bind:this={ref1}>
            {#each chars1 as char, i}
                <span class='char'>{char === ' ' ? '\u00A0': char}</span>
            {/each}
        </p>
    </section>
    <section style='margin-bottom: 500px;'>
        <h1>HTML-Ipsum Info 2</h1>
        <p class='animated-text' bind:this={ref2}>
            {#each chars2 as char, i}
                <span class='char'>{char === ' ' ? '\u00A0': char}</span>
            {/each}
        </p>
    </section>
</div>

<style>
    .main {
        background: #000;
        color: #fff;
        display: absolute;
        top: 0;
        left: 0;
        padding: 10px;
    }

    section {
        display: block;
        margin: 400px 200px
    }

    h1 {
        font-size: 72px;
    }

    p {
        font-size: 24px;
    }

    .animated-text {

    }

    .char {
        display: inline-block;
        opacity: 1;
        transform: translateY(40px);
    }
</style>