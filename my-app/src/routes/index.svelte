<script context="module">
    import {usageDataAggregator, vMFactory} from '../core/main';
    import UsageDataTable from '../components/UsageDataTable.svelte';

    let gasData = [];
    let powerData = [];
    gasData = [...vMFactory.createRecordingVM(usageDataAggregator.getUsageData('gas'))];
    powerData = vMFactory.createRecordingVM(usageDataAggregator.getUsageData('power'));

    export async function preload() {
        const res = await this.fetch(`records/getAll`, {
            credentials: 'include'
        });

        let data = await res.json();

        usageDataAggregator.updateUsageData(data);
        gasData = [...vMFactory.createRecordingVM(usageDataAggregator.getUsageData('gas'))];
        powerData = vMFactory.createRecordingVM(usageDataAggregator.getUsageData('power'));
    }
</script>

<svelte:head>
    <title>Sapper project template</title>
</svelte:head>

<UsageDataTable powerData="{powerData}" gasData="{gasData}"></UsageDataTable>
