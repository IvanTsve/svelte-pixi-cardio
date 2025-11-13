<div bind:this={container}>

</div>
<script >
    import * as PIXI from 'pixi.js';
    import {onMount} from 'svelte';
    import run1 from '$lib/assets/walk/1.png';
    import run2 from '$lib/assets/walk/2.png';
    import run3 from '$lib/assets/walk/3.png';
    import run4 from '$lib/assets/walk/4.png';
    import run5 from '$lib/assets/walk/5.png';
    import run6 from '$lib/assets/walk/6.png';
    import one from '$lib/assets/slash/1.png';
    import two from '$lib/assets/slash/2.png';
    import three from '$lib/assets/slash/3.png';
    import four from '$lib/assets/slash/4.png';
    import five from '$lib/assets/slash/5.png';
    import six from '$lib/assets/slash/6.png';
    import shieldOne from '$lib/assets/shield/1.png';
    import shieldTwo from '$lib/assets/shield/2.png';
    import shieldThree from '$lib/assets/shield/3.png';

    let container;
    let app;
    let isRunning = false;
    let frame = 0;
    let frameTicker;
    let textures = {
        walk: [],
        slash: [],
        shield: []
    };
    let slashFrame = 0;
    let slashTicker;
    let isSlashing = false;

    onMount(() => {
        console.log('the component has mounted');
        app = new PIXI.Application({
            background: '#1099bb',
            resizeTo: window,
        });
        container.appendChild(app.view);
        textures['walk'].push(
            PIXI.Texture.from(run1),
            PIXI.Texture.from(run2),
            PIXI.Texture.from(run3),
            PIXI.Texture.from(run4),
            PIXI.Texture.from(run5),
            PIXI.Texture.from(run6),
        );
        textures['slash'].push(
            PIXI.Texture.from(one),
            PIXI.Texture.from(two),
            PIXI.Texture.from(three),
            PIXI.Texture.from(four),
            PIXI.Texture.from(five),
            PIXI.Texture.from(six),
        );
        textures['shield'].push(
            PIXI.Texture.from(shieldOne),
            PIXI.Texture.from(shieldTwo),
            PIXI.Texture.from(shieldThree),
        );

        const hero = new PIXI.Sprite(textures['walk'][1]);
        app.stage.addChild(hero);


        window.addEventListener('keydown', (e) => {
            if (e.code === 'KeyD') {
                handleRight(hero);
            } 
            if (e.code === 'KeyA') {
                handleLeft(hero);
            }
            if (e.code == 'Space') {
                handleSlash(hero);
            }
            if (e.code == 'KeyS') {
                handleShield(hero);
            }
        });

        window.addEventListener('keyup', (e) => {
            if (e.code === 'KeyD' || e.code === 'KeyA') {
                stopWalk(hero);
            }
            if (e.code == 'Space') {
                setTimeout(() => {
                    handleStopSlash(hero);

                }, 100);
            }
            if (e.code == 'KeyS') {
                setTimeout(() => {
                    handleStopSlash(hero);
                }, 100);
            }
        });

    });

    function handleStopSlash(hero) {
        clearInterval(slashTicker);
        isSlashing = false;
        slashFrame = 0;
        hero.texture = textures['walk'][0];
    }

    function handleShield(hero) {
        hero.scale.x = 1;
        hero.anchor.x = 0;
        if (isSlashing) return;
        isSlashing = true;
        slashTicker = setInterval(() => {
            slashFrame = (slashFrame +1) % textures['shield'].length;
            hero.texture = textures['shield'][slashFrame];
        },100) 
        
    }

    function handleSlash(hero) {
        hero.scale.x = 1;
        hero.anchor.x = 0;
        if (isSlashing) return;
        isSlashing = true;
        slashTicker = setInterval(() => {
            slashFrame = (slashFrame +1) % textures['slash'].length;
            hero.texture = textures['slash'][slashFrame];
        },50) 
        
    }

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
            frame = (frame + 1) % textures['walk'].length;
            hero.texture = textures['walk'][frame];
        }, 200);
    }

    function stopWalk(hero) {
        isRunning = false;
        clearInterval(frameTicker);
        hero.texture = textures['walk'][0];
    }


</script>
