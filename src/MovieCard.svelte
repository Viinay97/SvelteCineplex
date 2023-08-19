<script>
    export let movie;
    export let onMovieClick;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="movie" on:click={() => onMovieClick(movie)}>
    <div>
        <p>{movie.Year}</p>
    </div>
    <div>
        <img src={movie.Poster !== 'N/A' ? movie.Poster : 'http://via.placeholder.com/400'} alt="" />
    </div>
    <div>
        <h3>{movie.Title}</h3>
        <span>{movie.Type}</span>
    </div>
</div>
