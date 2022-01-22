<script context="module">
    import { dataset_dev, each } from "svelte/internal";
    let key = process.env.MOVIE_DB_TOKEN;

    export async function load({ fetch, params }){
        const res = await fetch(
            `https://api.themoviedb.org/3/search/movie?api_key=${key}&language=en-US&query=${params.id}&page=1&include_adult=false`
        );
        const data = await res.json();
        if (res.ok) {
            return{
                props: { searchedMovie: data.results }
            }
        }
    }
</script>

<script>
    import MovieCard from "../../components/MovieCard.svelte";
    import { fly } from 'svelte/transition';
    export let searchedMovie;
</script>

<div in:fly={{ y: 50, duration: 500, delay: 500}} out:fly={{duration: 500}} class="searched-movies">
    {#each searchedMovie as movie}
    <MovieCard {movie} />
    {/each}
</div>

<style>
    .searched-movies {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(175px, 1fr));
        column-gap: 1rem;
        row-gap: 3rem;
    }
</style>

