<script>
    export let message = "Loading...";
    export let type = "bot";
</script>

{#if type === "bot"}
    <div class="ai">
        {message}
    </div>
{:else}
    <div class="human">
        {message}
    </div>
{/if}

<style>
    div {
        border-radius: 1rem;
        padding: 1rem;
        display: inline-block;
        white-space: pre-line;
    }
    .ai {
        background-color: #c23c3c;
        color: #d4d4d4;
        border-bottom-left-radius: 0;
    }
    .human {
        background-color: #eeeeee;
        border-bottom-right-radius: 0;
        float: right;
        margin-bottom: 1rem;
    }
</style>