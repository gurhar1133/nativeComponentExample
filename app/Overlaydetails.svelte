<script>
    import { closeModal } from 'svelte-native'
    import Button from './Button.svelte';
    import Card from "./Card.svelte";
    import Overlay from "./Overlay.svelte";
    import Textfield from "./Textfield.svelte";

    export let data;
    export let type;

    let components = {"Button": Button, "Textfield": Textfield, "Card": Card,
         "Overlay": Overlay};

    console.log("Details component type:", typeof type);
    console.log("Details component data:", typeof data);

</script>

<style>

</style>
<frame id="overlay-detail">
    <page class="bg-gray-800 bg-opacity-50 z-50 absolute top-0 h-screen"  enableSwipeBackNavigation={true}>
       <scrollView>
        <stackLayout>
            <svelte:component this={components[type]} {...data}/>
            <button on:tap={()=>{
                closeModal("closing modal");
                }}> CLOSE </button>
        </stackLayout>
       </scrollView> 
        
    </page>
</frame>
    
     
    
               
