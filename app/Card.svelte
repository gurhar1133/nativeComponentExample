<script>
    import {Color} from "tns-core-modules/color";
    export let shaped = false;
    export let hasImage = false;
    export let imgSrc;
    export let title;
    export let subtitle;
    export let description;
    export let elevation;
    export let bonus = false;
    let card;
    
    const platformModule = require("tns-core-modules/platform");

    let platform = platformModule.isIOS ? "ios" : "android";
    let androidShadowClass;
    if (platform === "android"){ // manipulating classes for android

        if (elevation === "sm"){
            androidShadowClass = "1";
        }
        else if(elevation === "lg"){
            androidShadowClass = "8";
        }
        else if (elevation === "md"){
            androidShadowClass = "4";
        }
        else if (elevation === "xl"){
            androidShadowClass = "12";
        }
    
    }

    let card_type = "card-no-image"
    if (hasImage){card_type = "card"}
    if (shaped){card_type = card_type + " card-shaped"}

    let card_class_template = `${card_type} border bg-white border-gray-500 my-2 mx-2 max-w-md w-5/6 rounded`;
    
    function onLoaded(args){
        const view = args.object;
        card = view.getViewById("card");
        if (platform === "ios"){
            const iosUIView = view.ios;
            // iosUIView.layer.shadowColor = UIColor.blackColor.CGColor;
            iosUIView.layer.shadowColor = new Color("black").ios.CGColor;
            iosUIView.layer.shadowOpacity = .25;
            iosUIView.layer.shadowOffset = CGSizeMake(2,8);
            console.log(iosUIView);
        }
    }

    function onTap(args){
        if (bonus){
            console.log("bonus card");
            card.animate({
                scale: {x: 1.3, y: 1.3},
                duration: 200
            }).then(()=>{
                card.animate({
                    scale: {x: 1, y: 1},
                    duration: 200
                })
            })
        }
    }

</script>

<style>
.card{
    /* padding: 1; */
    /* margin: 2; */
    /* height: 300; */
    /* width: 200; */
    /* border-color: #555; */
    /* border-width: 1;
    border-radius: 20; */
}
.card-shaped{
    /* TODO: shape the edges */
    border-radius: 30 0 30 0;
}
.card-no-image{
    /* padding: 1; */
    /* margin: 2; */
    /* border-color: #555;
    border-width: 1;
    border-radius: 20; */
    /* height: 300; */
    /* width: 200; */
}

</style>
<stackLayout id="card" on:loaded="{onLoaded}" >
<stackLayout  on:tap={onTap}  class="{card_class_template}" horizontalAlignment="center" androidElevation="{androidShadowClass}">
    {#if hasImage}
        {#if imgSrc === "https://qph.fs.quoracdn.net/main-qimg-40ccab97c4b182082c3525bb34575a37.webp"}
            <image class="h-52 w-full " src="https://i.redd.it/1xlrjb24x4f41.jpg" alt=""/>
        {:else}
            <image class="h-52 w-full " src="{imgSrc}" alt=""/>
        {/if}
    {/if}
    <label class="px-2 text-gray-800 text-2xl">{title}</label>
    <label class="px-2 pb-4 text-gray-700 text-xl">{subtitle}</label>
    <label class="px-2 pb-3 text-gray-700 text-base">{description}</label>
    <slot></slot>
</stackLayout>

</stackLayout> 
