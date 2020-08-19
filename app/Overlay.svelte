<script>
    
    import Overlaydetails from "./Overlaydetails.svelte";
    import { showModal } from "svelte-native";
    
    
    var dialogs = require("tns-core-modules/ui/dialogs");
    
    export let absolute = false; 
    export let opacity = .45;
    export let zIndex = "10"; 
    export let value = true;
    export let markup;
    export let modalMessage;
    export let component;

    
    //console.log("type of opacity: ", typeof opacity, opacity);
    

    let frame;
    let closeCallback;
    let bgOpacity;
   
    if (opacity >= 0 && opacity < .25){
        bgOpacity = "bg-opacity-25";
    }
    else if (opacity >= .25 && opacity < .50){
         bgOpacity = "bg-opacity-50";
    }
    else if (opacity >= .50 && opacity < 1){
        bgOpacity = "bg-opacity-75";
    }
    else if (opacity >= 1){
        bgOpacity = "bg-opacity-100";
    }
    else{
        //console.log('overlay ERROR');
    }

    
    // $: if (!absolute && !value){
    //     closeModal('hi from modal');
    // }
    const platformModule = require("tns-core-modules/platform");
    let platform = platformModule.isIOS ? "ios" : "android";

   // $: console.log("overlay value: ",value);

    let sizing = absolute ? "h-full w-full absolute" : "w-full width-full modal-backdrop-full fixed";
    let overlay_template = `${sizing} bg-gray-800 ${bgOpacity}`;

    
    $: if (value){
       // console.log("open overlay");
    }

    async function launchModal(){
        let result = await showModal({
	        page: Overlaydetails,
            props: {
                type: component.type,
                data: component.props
            }
        })
    }

    $: if (value && !absolute){
        console.log("navigating to overlay");
        launchModal();
        value = false;
    }
</script>

<style>
.modal-backdrop-full{
        /* top: 0; */
    }
.the-top{
    z-index: 100;
}
</style>

{#if value && absolute}
    <absoluteLayout on:loaded={()=>{
        //console.log("opacity result:",bgOpacity);
    }} class="{overlay_template}">
    <absoluteLayout top="100" left="60">
        <slot></slot>
    </absoluteLayout>
    
    </absoluteLayout>

   
<!-- {:else if value && !absolute }
    -->

    
	

{/if}