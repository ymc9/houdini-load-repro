<script lang="ts">
    import { graphql } from '$houdini';
    import client from '../client';
    client.init();

    const film = graphql`
        query Film {
            film(id: "wrong-movie-id") {
                id
                title
            }
        }
    `;

    // $: film.fetch();

    $: console.log($film);
</script>

{#if $film?.errors}
    <p>Error: {$film.errors[0].message}</p>
{:else if $film?.data}
    <h1>Movie: {$film.data.film.title}</h1>
{/if}

<slot />
