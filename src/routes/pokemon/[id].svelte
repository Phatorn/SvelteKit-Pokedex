<script lang="ts" context="module">
    export async function load({params}: any) {
        const id = params.id
        const url = `https://pokeapi.co/api/v2/pokemon/${id}`
        const res = await fetch(url)
        const pokeman = await res.json()
        return {props: {pokeman}}
    }
</script>
<script lang="ts">
    export let pokeman: any
    const type = pokeman.types[0].type.name
</script>
<div class="flex flex-col items-center">
    <h1 class="text-4xl text-center my-8 uppercase">{pokeman.name}</h1>
    <p>
        Type: <strong>{type}</strong> 
        | Height: <strong>{pokeman.height}</strong>
        | Weight: <strong>{pokeman.weight}</strong>
    </p>
    <img class="h-40 w-40 card-image" src="{pokeman.sprites['front_default']}" alt={pokeman.name}>
</div>