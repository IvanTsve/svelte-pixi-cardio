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
    let isRunning = false;
    let frame = 0;
    let frameTicker;
    let textures = [];

    onMount(() => {
        console.log('the component has mounted');
        app = new PIXI.Application({
            background: '#1099bb',
            resizeTo: window,
        });
        container.appendChild(app.view);
        textures.push(
            PIXI.Texture.from(run1),
            PIXI.Texture.from(run2),
            PIXI.Texture.from(run3),
        );

        const hero = new PIXI.Sprite(textures[1]);
        app.stage.addChild(hero);


        window.addEventListener('keydown', (e) => {
            if (e.code === 'KeyD') {
                handleRight(hero);
            } 
            if (e.code === 'KeyA') {
                handleLeft(hero);
            }
        });

        window.addEventListener('keyup', (e) => {
            if (e.code === 'KeyD' || e.code === 'KeyA') {
                stopWalk(hero);
            }
        });

    });
    function handleRight(hero) {
        hero.scale.x = 1;
        hero.anchor.x = 0;
        hero.x += 25; 
        loopWalk(hero);
    }
    function handleLeft(hero) {
        hero.scale.x = -1;
        hero.anchor.x = 1;
        hero.x -= 25; 
        loopWalk(hero);
    }

    function loopWalk(hero) {
        if (isRunning) return; 
        isRunning = true;

        frameTicker = setInterval(() => {
            frame = (frame + 1) % textures.length;
            hero.texture = textures[frame];
        }, 200);
    }

    function stopWalk(hero) {
        isRunning = false;
        clearInterval(frameTicker);
        hero.texture = textures[0];
    }


</script>
