<script>
    import Card from './Card.svelte'
    import Loader from './Loader.svelte'
    export let posts = [];
</script>

<style>
  .Timeline {
    padding: 4em 0 0 0;
  }
</style>

<div class="Timeline">
    <div class="Timeline-container">
        {#each posts as post}
            <Card {...post} />
        {:else}
            <Loader />
        {/each}
    </div>
</div>