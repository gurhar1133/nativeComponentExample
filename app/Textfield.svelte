<script>
    import {createEventDispatcher} from 'svelte';
    export let placeHolder;
    export let filled = false;
    export let outlined = false;
    export let value;

    const dispatch = createEventDispatcher();
    let bgColor = filled ? "bg-gray-400 bg-opacity-25 filled-border" : "";
    let outline = outlined ? "outline-border" : "";
    $: console.log(value);

    let text_template = `mx-2 my-2 py-4 px-3 ${bgColor} ${outline}`;
    function onReturn(){
        dispatch("enter", value);
    }

</script>

<style>
    .filled-border{
        /* border-width: 0; */
        /* border-color: white; */
        border-radius: 10 10 0 0;
    }
    .outline-border{
        border-width: 2;
        border-radius: 10 10 10 10;
    }
</style>

<textField on:returnPress={onReturn}
            hint="{placeHolder}" 
            class="{text_template}"
            bind:text="{value}"></textField>