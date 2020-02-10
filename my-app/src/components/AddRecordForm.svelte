<script>
    export let type;
    export let cb;
    let date;
    let value;

    function send_add_post() {
        fetch(`http://localhost:3000/records/add?type=${type}&value=${value}&date=${date}`, {method: 'POST'})
                .then(() => {
                    cb({type, date, value});

                });
        // cb({type, date, value});
    }
</script>

<form on:submit|preventDefault={send_add_post}>
    <input type="hidden" name="type" value="{type}" id="type">
    <input type="text" name="value" id="value" bind:value={value}>
    <input type="text" name="date" id="date" bind:value={date}>
    <input type="submit">
</form>
