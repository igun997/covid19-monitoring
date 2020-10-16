<script>
    import Card, {Content, PrimaryAction, Media, MediaContent, Actions, ActionButtons, ActionIcons} from '@smui/card';
    import Button, {Label} from '@smui/button';
    import IconButton, {Icon} from '@smui/icon-button';
    import List, {Item, Text} from '@smui/list';
    import numeral from "numeral"
    export let bindData;
    let toParent = {
        title:"Tentang Pengembang"
    };
    console.log(bindData)
    if ('function' === typeof bindData) {
        bindData(toParent);
    }
</script>
<style>
    .gap {
        margin-top: 10px;
    }
</style>

<div class="gap">
    <Card>
        <Content>
            Gabut Pak
        </Content>
    </Card>
</div>
