<script>
    let year = 2020;
    let month = 12;
    export let date;
    export let cb;

    function addMonth(event) {
        month += 1;
        if (month > 12) {
            year++;
            month = 1;
        }
        date = new Date(year + '-' + month + '-01');
        cb();
    }

    function subtractMonth(event) {
        month -= 1;
        if (month < 1) {
            year--;
            month = 12;
        }
        date = new Date(year + '-' + month + '-01');
        cb();
    }
</script>


<button on:click={subtractMonth}>earlier</button>
date: {date.toLocaleDateString('en-US', {year: 'numeric', month: 'short'})}
<button on:click={addMonth}>later</button>

