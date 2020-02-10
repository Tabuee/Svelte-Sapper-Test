<script>
    import DataTable from '../components/DataTable.svelte';
    import AddRecordForm from '../components/AddRecordForm.svelte';
    import {usageDataAggregator, vMFactory} from '../core/main';
    import DatePicker from '../components/DatePicker.svelte';

    export let gasData;
    export let powerData;
    let dateFrom = new Date('2018-08-01');
    let dateTo = new Date('2020-12-01');

    let fieldNames = ['type', 'month', 'value', 'costs', 'change', 'diff'];
    let updateCb = (element) => {
        console.log(dateFrom, dateTo, 'first');

        if (element) {
            usageDataAggregator.addUsageData(element.type, {value: parseInt(element.value), month: element.date});
        }
        gasData = [...vMFactory.createRecordingVM(usageDataAggregator.getUsageDataInRange('gas', dateFrom, dateTo))];
        powerData = vMFactory.createRecordingVM(usageDataAggregator.getUsageDataInRange('power', dateFrom, dateTo));

        console.log(usageDataAggregator.getUsageData('gas'));
    }

</script>

<h3>From</h3>
<DatePicker bind:date={dateFrom} cb="{updateCb}"></DatePicker><br>

<h3>To</h3>
<DatePicker bind:date={dateTo} cb="{updateCb}"></DatePicker>

<hr>

<h1>Gas</h1>
<DataTable bind:fieldNames={fieldNames} bind:items="{gasData}"></DataTable>
<AddRecordForm type="gas" cb="{updateCb}"></AddRecordForm>

<h1>Power</h1>
<DataTable fieldNames="{fieldNames}" items="{powerData}"></DataTable>
<AddRecordForm type="power" cb="{updateCb}"></AddRecordForm>
