<div>
    <Slots bind:this={slotsRef} />
    <div class="button-container">
        <Button {handleSpin}   />
    </div>

</div>

<script>
    import Slots from "$lib/components/slots.svelte";
    import Button from '$lib/components/button.svelte';

    let spinning = false;
    let slotsRef;

    function handleSpin() {
        if (slotsRef) {
            slotsRef.handleLoop();
        }
    }   
   
</script>

<style>
    .button-container {
        margin-top: 20px;
        text-align: center;
    }

</style>