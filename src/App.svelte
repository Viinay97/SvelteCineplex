<script>
    import { onMount } from "svelte";
    import MovieCard from "./MovieCard.svelte";

	const API_KEY = '731333ac';
    const API_URL = `https://www.omdbapi.com?apikey=${API_KEY}`;
    

    let searchTerm = "";
    let movies = [];

    onMount(() => {
        searchMovies('Avengers');
    });

    async function searchMovies(title) {
        const response = await fetch(`${API_URL}&s=${title}`);
        const data = await response.json();
        movies = data.Search;
    }

    async function getMovieDetail(imdbId) {
        showMovieModal = true;
        const response = await fetch(`${API_URL}&i=${imdbId}`);
        const data = await response.json();
        console.log(data);
    }
</script>

<div class="app">
    <h1>SvelteCineplex</h1>
    <div class="search">
        <input 
            bind:value={searchTerm}
            placeholder="Search for Movies" 
        />
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div on:click={() => searchMovies(searchTerm)}>
            <i class="uil uil-search searchIcon"></i>
        </div>
    </div>
    {#if movies.length > 0}
        <div class="container">
            {#each movies as movie}
                <MovieCard movie={movie} onMovieClick={() => getMovieDetail(movie.imdbID)}/>
            {/each}
        </div>
    {:else}
        <div class="empty">
            <h2>No Movies Found</h2>
        </div>
    {/if}
</div>
