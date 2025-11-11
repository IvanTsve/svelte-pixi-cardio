<button on:click={handleSpin}>spin</button>
<script>
    let { handleSpin } = $props();
</script>
<style>
    button {
        background: linear-gradient(90deg, #ff6a00, #ee0979);
        color: white;
        border: none;
        border-radius: 25px;
        padding: 0.75em 2em;
        font-size: 1.2em;
        font-weight: bold;
        box-shadow: 0 4px 14px rgba(0,0,0,0.15);
        cursor: pointer;
        transition: transform 0.2s, box-shadow 0.2s;
    }
    button:hover {
        transform: scale(1.05);
        box-shadow: 0 6px 20px rgba(0,0,0,0.25);
    }
</style>
