<script>
    import Button from "$lib/components/button.svelte";
    function handleSpin() {
        console.log("Spin button clicked!");
    }
</script>

<div class="main">
    <Button {handleSpin} />
</div>

<style>
    .main {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: #f0f0f0;
    }
</style>
