<div class="slots" bind:this={container}>
</div>

<script>
    import * as PIXI from 'pixi.js';
    import {onMount} from 'svelte';
    import one from '$lib/assets/slots/1.png';
    import two from '$lib/assets/slots/2.png';
    import three from '$lib/assets/slots/3.png';
    import four from '$lib/assets/slots/4.png';
    import five from '$lib/assets/slots/5.png';
    import six from '$lib/assets/slots/6.png';
    import seven from '$lib/assets/slots/7.png';
    import eight from '$lib/assets/slots/8.png';    
    import nine from '$lib/assets/slots/9.png';
    import ten from '$lib/assets/slots/10.png';
    import eleven from '$lib/assets/slots/11.png';
    import twelve from '$lib/assets/slots/12.png';
    import thirteen from '$lib/assets/slots/13.png';
    import fourteen from '$lib/assets/slots/14.png';
    import fifteen from '$lib/assets/slots/15.png';
    let container;
    let app;
    let textures = [];
    const SPRITE_WIDTH = 80;  // Set to your desired width
    const SPRITE_HEIGHT = 80;
    let rows = [];
    let isSpining = false;

    onMount(() => {
        app = new PIXI.Application({
            width: 800,
            height: 600,
            backgroundColor: 0x1099bb,
        })
        container.appendChild(app.view);

        textures = [
            PIXI.Texture.from(one),
            PIXI.Texture.from(two),
            PIXI.Texture.from(three),
            PIXI.Texture.from(four),
            PIXI.Texture.from(five),
            PIXI.Texture.from(six),
            PIXI.Texture.from(seven),
            PIXI.Texture.from(eight),
            PIXI.Texture.from(nine),
            PIXI.Texture.from(ten),
            PIXI.Texture.from(eleven),
            PIXI.Texture.from(twelve),
            PIXI.Texture.from(thirteen),
            PIXI.Texture.from(fourteen),
            PIXI.Texture.from(fifteen),
        ];

        rows = [
            [
                new PIXI.Sprite(textures[0]),
                new PIXI.Sprite(textures[1]),
                new PIXI.Sprite(textures[2]),
            ],
            [
                new PIXI.Sprite(textures[3]),
                new PIXI.Sprite(textures[4]),
                new PIXI.Sprite(textures[5]),
            ],
            [
                new PIXI.Sprite(textures[6]),
                new PIXI.Sprite(textures[7]),
                new PIXI.Sprite(textures[8]),
            ],
        ]
        rows.forEach((row, rowIndex) => {
            row.forEach((sprite, index) => {
                sprite.x = index * (SPRITE_WIDTH + 245);
                sprite.y = 50 + rowIndex * (SPRITE_HEIGHT + 100);
                app.stage.addChild(sprite);
            });
        });
    });

    export function handleLoop() {
        if (isSpining == true) {
            return;
        }
        console.log('Spin buttonclicked');

        isSpining = true;
        let interval = setInterval(() => {
            rows.forEach((row, rowIndex) => {
                row.forEach((sprite, index) => {
                    sprite.y += 10;
                    if (sprite.y == 680) {
                        sprite.y = 0;
                    }
                });
            });
        }, 50);

        let timeout = setTimeout(() => {
            isSpining = false;
            clearInterval(interval);
            clearTimeout(timeout);
        }, 5000);
    }
</script>

<style>
    .slots {
        margin: 0 auto;
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>