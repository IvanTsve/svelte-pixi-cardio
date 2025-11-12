<div bind:this={container}>

</div>
<script >
    import * as PIXI from 'pixi.js';
    import {onMount} from 'svelte';
    import run1 from '$lib/assets/run1.png';
    import run2 from '$lib/assets/run2.png';
    import run3 from '$lib/assets/run3.png';

    let container;
    let app;
    let running = {
        run1: null,
        run2: null,
        run3: null,
    }

    onMount(() => {
        console.log('the component has mounted');
        app = new PIXI.Application({
            background: '#1099bb',
            resizeTo: window,
        });
        container.appendChild(app.view);

        const textures = [
            PIXI.Texture.from(run1),
            PIXI.Texture.from(run2),
            PIXI.Texture.from(run3),
        ];

        const run1Sprite = new PIXI.Sprite(textures[0]);
        app.stage.addChild(run1Sprite);
        

    });

</script>
