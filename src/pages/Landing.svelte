<script>
    import Card, {Content, PrimaryAction, Media, MediaContent, Actions, ActionButtons, ActionIcons} from '@smui/card';
    import Button, {Label} from '@smui/button';
    import IconButton, {Icon} from '@smui/icon-button';
    import List, {Item, Text} from '@smui/list';
    import numeral from "numeral"
    export let bindData;
    let toParent = {
        title:"Beranda"
    };
    console.log(bindData)
    if ('function' === typeof bindData) {
        console.log("PassIt")
        bindData(toParent);
    }
    let total_case = {
        conf:0,
        death:0,
        recover:0
    };
    async function getCovid() {
        const req = await fetch("https://covid19.mathdro.id/api",{
            method:"GET",
            headers:{
                "Accept":"application/json"
            }
        });

        return  await req.json();

    }
</script>
<style>
    .gap {
        margin-top: 10px;
    }
</style>
<div class="card-container short">
    <div class="gap">
        <Card>
            <Content>
                <h4>Positif Covid</h4>
                {#await getCovid()}
                    <h1 align="center">Loading . . .</h1>
                {:then data}
                    <h1 align="center">{numeral(data.confirmed.value).format("0,0")} Orang</h1>
                {/await}
            </Content>
            <Actions>
                <IconButton class="material-icons" title="More options">more_vert</IconButton>
            </Actions>
        </Card>
    </div>
    <div class="gap">
        <Card>
            <Content>
                <h4>Sembuh Dari Covid</h4>
                {#await getCovid()}
                    <h1 align="center">Loading . . .</h1>
                {:then data}
                    <h1 align="center">{numeral(data.recovered.value).format("0,0")} Orang</h1>
                {/await}
            </Content>
            <Actions>
                <IconButton class="material-icons" title="More options">more_vert</IconButton>
            </Actions>
        </Card>
    </div>
    <div class="gap">
        <Card>
            <Content>
                <h4>Modar Dari Covid</h4>
                {#await getCovid()}
                    <h1 align="center">Loading . . .</h1>
                {:then data}
                    <h1 align="center">{numeral(data.deaths.value).format("0,0")} Orang</h1>
                {/await}
            </Content>
            <Actions>
                <IconButton class="material-icons" title="More options">more_vert</IconButton>
            </Actions>
        </Card>
    </div>
</div>
