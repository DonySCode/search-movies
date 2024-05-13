<script>
    import Movie from "./Movie.svelte";

    let value = ''
    let response = []

    //Tomando el valor de cada vez que se teclea
    const handleInput = (event) => 
    value = event.target.value

     $: if(value.length > 2) {
        response = fetch(`https://www.omdbapi.com/?s=${value}&apikey=6191dc93`)
        .then(res => res.json())
        .then(apiResponse => apiResponse.Search || [])
    }
</script>

<input placeholder="Search movies..." 
value={value} 
on:input={handleInput} 
/>

<!--Renderizado Condicional-->
{#await response} 
    <strong>Loading...</strong>
{:then movies}
    {#each movies as {Title, Poster, Year}}
        <Movie title={Title} poster={Poster} year={Year} />
    {:else}
        <strong>No hay resultados</strong>
    {/each}
{/await}


