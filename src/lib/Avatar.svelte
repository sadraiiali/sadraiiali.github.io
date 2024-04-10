<script>
    import { onMount } from 'svelte';
    import { Motion, useAnimation } from "svelte-motion";
    
    const boxNumber = 40;
    const pixelSize = 6;

    const controls = useAnimation();
    const boxes = Array(boxNumber * boxNumber).fill().map(
        (_, i) => ({ key: i, i: Math.floor(i / boxNumber), j: i % boxNumber })
    );
    let colors = [];

    onMount(async () => {
        const img = new Image();
        img.src = '/img/alireza-sadraii.jpg';
        await img.decode();

        const canvas = document.createElement('canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = img.width;
        canvas.height = img.height;
        ctx.drawImage(img, 0, 0);
        const resizeRate = img.width /(boxNumber);
        boxes.forEach((box) => {
            const pixelData = ctx.getImageData(box.j*resizeRate, box.i*resizeRate, 1, 1).data;
            
            colors[box.key] = `rgb(${pixelData[0]},${pixelData[1]},${pixelData[2]})`;
        });
    });

    const click = (origin) => async () => {
        const delay = (box) => Math.sqrt(Math.pow(box.i - origin.i, 2) + Math.pow(box.j - origin.j, 2) + 30 * Math.random()) * 0.03;

        await controls.start((box) => ({
            opacity: 0,
            transition: { delay: delay(box) },
        }));

        await controls.start((_) => ({
            x: (Math.random() - 0.5) * 1000,
            y: (Math.random() - 0.5) * 1000,
            transition: { duration: 0.01 },
        }));

        controls.start((box) => ({
            opacity: 1,
            x: 0,
            y: 0,
            transition: { duration: 1, delay: delay(box) },
        }));
    };
</script>

<style>
    .smallgrid {
        display: grid;
        grid-template-columns: repeat(20, auto);
        gap:0;
        background-color: white;
    }
    .smallbox {
        width: 6px;
        height: 6px;
    }
</style>

<div class="smallgrid" 
     style:width={boxNumber * 6 +"px"}
     style="grid-template-columns: repeat({boxNumber}, auto);">

    {#each boxes as box (box.key)}
        <Motion let:motion 
                custom={box} 
                animate={controls}>
            <div class="smallbox" 
                 use:motion 
                 on:click={click(box)} 
                 style="background-color: {colors[box.key]}" />
        </Motion>
    {/each}

</div>