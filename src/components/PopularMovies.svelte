<script>
    export let popular;
    import MovieCard from './MovieCard.svelte';
</script>

<h3>Popular Movies</h3>
<div class="popular-movies">
    {#each popular as movie}
        <MovieCard {movie} />
    {/each}
</div>

<style>
    h3 {
        padding: 0 1rem;
    }
    .popular-movies {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(175px, 1fr));
        column-gap: 1rem;
        row-gap: 3rem;
    }
</style>