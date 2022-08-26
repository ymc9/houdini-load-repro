<script lang="ts">
    import { graphql } from '$houdini';
    import client from '../client';
    client.init();

    const film = graphql`
        query Film {
            film(id: "ZmlsbXM6MQ==") {
                id
                title
            }
        }
    `;

    $: console.log($film?.data?.film);
</script>

{#if $film?.data}
    <h1>Movie: {$film.data.film.title}</h1>
{:else if $film?.errors}
    <p>Error</p>
{/if}
<slot />
