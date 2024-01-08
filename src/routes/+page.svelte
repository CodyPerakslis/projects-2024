<script lang="ts">
    import Week01 from './week01/+page.svelte'

    let week = 1;

    const weekPages = [Week01];

    async function handleKeyDown(event: KeyboardEvent) {
        if (event.key === 'ArrowRight' || event.key === 'ArrowDown') {
            event.preventDefault();
            week += 1;
        }
        if (event.key === 'ArrowLeft' || event.key === 'ArrowUp') {
            event.preventDefault();
            week -= 1;
        }
        if (week < 1) {
            week = 1;
        }
        if (week > 52) {
            week = 52;
        }
    }
</script>

<h1 class="title">Weekly Projects - 2024</h1>
<input on:keydown={handleKeyDown} class="weeks" type="range" min="1" max="52" step="1" bind:value={week} />

{#each weekPages as page, i}
    {#if i + 1 === week}
    <div class="week-info">
        <svelte:component this={page} />
    </div>
    {/if}
{/each}

{#if weekPages.length < week}
    <h2 class="missing-week">Week {week} is not yet available.</h2>
{/if}


<style>
    .title {
        text-align: center;
        font-size: 50px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        color: #04AA6D;
    }
    .weeks {
        position: absolute;
        transform: rotate(90deg);
        top: 50vh;
        left: -40vh;
        width: 90vh;
    }
    .weeks::-webkit-slider-thumb {
        -webkit-appearance: none;
        appearance: none;
        width: 25px;
        height: 25px;
        background: #04AA6D;
        cursor: pointer;
    }
    .week-info {
        border: solid 20px;
        padding: 20px;
        margin-top: 20px;
        width: 70%;
        margin-left: 15%;
        margin-right: 15%;
        background-color: aliceblue;
        border-radius: 10%;
    }
    .missing-week {
        text-align: center;
        font-size: 25px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
</style>
