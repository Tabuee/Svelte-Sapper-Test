<style>
</style>

<script>
    export let fieldNames;
    export let items;
</script>

<table>
    <thead>
    <tr>
        {#each fieldNames as name}
            <td>{name}</td>
        {/each}
    </tr>
    </thead>
    <tbody>
    {#each items as { ...fields }}
        <tr>
            {#each fieldNames as name}
                <td>{fields[name]}</td>
            {/each}
        </tr>
    {/each}
    </tbody>
</table>
