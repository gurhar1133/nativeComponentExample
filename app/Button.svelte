<script>
    import {createEventDispatcher} from "svelte";
    import {Color} from "color";
    export let btnText = "";
    export let color = 'purple';
    export let size = "md";
    export let elevation = "md";
    export let rounded = false;
    export let textMode = false;
    export let disabled = false;
    export let outline = false;
    export let fab = false;
    export let iconString;
    const platformModule = require("tns-core-modules/platform");
    const dispatch = createEventDispatcher();
    let iconTemplate = ``
    // establishing platform
    let platform = platformModule.isIOS ? "ios" : "android";

    // classes for the class template strings
    let actual_button;
    let tapX;
    let tapY;
    let wrapper;
    let circle;
    let backgroundColor;
    let textColor;
    let circleClass;
    let border;
    let borderRound = (rounded || fab) ? "rounded-heavy" : "rounded-light";
    let wrapperRounded;
    let sizeClass;
    let androidShadowClass = "4";
    let circle_top;
    let circle_left;

    btnText = btnText.toUpperCase();

    // manipulating the classes for ios
    // inelegant but going to define classes for ios and android completely separately
    // even if i repeat a lot of code
    if (platform === "ios"){
        // ios shadows:
        // import {Color} from "color";
        // import * as view from "ui/core/view";
        // wrapper.ios.layer.masksToBounds = false;
        // wrapper.ios.layer.shadowOpacity = 1.0;
        // wrapper.ios.layer.shadowRadius = 0.0;
        // wrapper.ios.layer.shadowColor = new Color('#000000').ios.CGColor;
        // wrapper.ios.layer.shadowOffset = CGSizeMake(2.0, 2.0);

        // size classes (still need definitions for fab)
        // Hard coded circle positions depending on the button size as well
        if (size === "sm"){
            sizeClass  = "smbtn";
            circle_top = "20";
            circle_left = "70";
            if (fab) {
                sizeClass = 'smfab';
                circle_top = "10";
                circle_left = "10";
            }
        }
        else if (size === "lg"){
            sizeClass  = "lgbtn";
            circle_top = "30";
            circle_left = "95";
            if (fab) {
                sizeClass = 'lgfab';
                circle_top = "20";
                circle_left = "20";
            }
        }
        else if (size === "md"){
            sizeClass = "mdbtn";
            circle_top = "25";
            circle_left = "80";
            if (fab) {
                sizeClass = 'smfab';
                circle_top = "10";
                circle_left = "10";
            }
        }
        else if (size === "xl"){
            sizeClass  = "xlbtn";
            circle_top = "40";
            circle_left = "110";
            //console.log("we have a large button");
            if (fab) {
               
            }
        }
        else if (size === "block"){
            sizeClass = "w-full"; 
            circle_top = "10";
            circle_left = "200";
        }

        // need shadow definitions for ios still


    } // FILL IN ANDROID FAB SIZING
    else if (platform === "android"){ // manipulating classes for android

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

        if (size === "sm"){
            sizeClass  = "smbtn";
            if (fab) {
                sizeClass = 'smfab';
                circle_top = "10";
                circle_left = "10";

            }
        }
        else if (size === "lg"){
            sizeClass  = "lgbtn";
            if (fab) {
                sizeClass = 'lgfab';
                circle_top = "20";
                circle_left = "20";
            }
        }
        else if (size === "md"){
            sizeClass = "mdbtn";
            if (fab) {
                sizeClass = 'smfab';
                circle_top = "10";
                circle_left = "10";
            }
        }
        else if (size === "xl"){
            sizeClass  = "xlbtn";
           // console.log("we have a large button");
            if (fab) {
               
            }
        }
        else if (size === "block"){
            sizeClass = "w-full"; 
        }

    }

    

    
    // coloring classes

    if(!outline && !textMode){
        textColor = 'text-white';
        border = "border-0";
        if (color === "primary"){
            backgroundColor = 'bg-blue-600';
        }
        else if (color === "secondary"){
            backgroundColor = 'bg-blue-300';
        }
        else {
            backgroundColor = `bg-${color}-500`;
        }
    }
    else if (outline){
        // error handling since we dont want both textmode and outline at same time
        textMode = false;
        backgroundColor = " bg-opacity-0";
        if (color === "primary"){
            textColor = 'text-blue-600 hover:bg-blue-200 hover:bg-opacity-25';
            border = "border-4 border-blue-600";
        }
        else if (color === "secondary"){
            textColor = 'text-blue-300 hover:bg-blue-200 hover:bg-opacity-25';
            border = "border-4 border-blue-300";
        }
        else {
            textColor = `text-${color}-500 hover:bg-${color}-200 hover:bg-opacity-25`;
            border = `border-4 border-${color}-500`;
        }
    }
    else if (textMode){
        // error handling since we dont want both textmode and outline at same time
        outline = false;
        backgroundColor = " bg-opacity-0";
        border = `border-0`;
        if (color === "primary"){
            textColor = 'text-blue-600 hover:bg-blue-200 hover:bg-opacity-5';
        }
        else if (color === "secondary"){
            textColor = 'text-blue-300 hover:bg-blue-200 hover:bg-opacity-5';
        }
        else {
            textColor = `text-${color}-500 hover:bg-${color}-200 hover:bg-opacity-5`;
            
        }
    }
    
    if (disabled){
        backgroundColor = "bg-gray-300 bg-opacity-5";
        textColor = "text-gray-600"
    }
    
  
    // class templates

    let wrapper_class_template = `${border} ${borderRound} ${backgroundColor} overflow-hidden my-1 mx-1 ${wrapperRounded}`;

    let button_class_template = `${sizeClass} ${backgroundColor} ${textColor} ${border} ${borderRound}
                             focus:outline-none relative overflow-hidden my-auto mx-auto`;

    let android_button_template = `${sizeClass} ${border} ${borderRound} ${backgroundColor} ${textColor}`;

    let fab_class_template = `relative ${sizeClass} ${backgroundColor} ${textColor} ${border} ${borderRound} my-1 mx-1 py-3 px-3`

    
    // todo: 
    //      Go through each class in templates
    //      Basic CSS templates
    // fix android border
    // fix both size + padding classes --> padding isnt best way to set button size for native; use height and width
    // fix android button border radius
    // fix ios circle border radius



    function onTouch(event){
        dispatch("tap");
        if(!disabled){
            // depending on the color
            if (size === "block"){
                console.log("block button has been clicked");

                if(actual_button){
                    console.log("block button is bound");
                    actual_button.animate({
                        scale: {x: 1.1, y: 1.1},
                        duration: 100
                    }).then(()=>{
                        actual_button.animate({
                            scale: {x: 1, y: 1},
                            duration: 100
                        })
                })
            }
            }
            else if (outline || textMode){
                if(color === "primary"){
                    circleClass = "circle-primary";
                }
                else if (color === "secondary"){
                    circleClass = "circle-secondary";
                }
                else if (color === 'purple'){
                    circleClass = "circle-purple";
                }
                else {
                    circleClass = "circle";
                }
            }
            else if (!(size === "block")){
                circleClass = "circle";
            }


            setTimeout(()=>{
                circleClass = "";
            }, 300);
        }
        if ((platform === "android" || fab ) && !disabled){
            if(actual_button){
                actual_button.animate({
                    scale: {x: 1.1, y: 1.1},
                    duration: 100
                }).then(()=>{
                    actual_button.animate({
                        scale: {x: 1, y: 1},
                        duration: 100
                    })
                })
            }
            
        }
        
            
    }

    function onLoaded(args){
        //console.log("button created");
        const view = args.object;
        actual_button = view.getViewById("button");
        //console.log("buttonView:", actual_button);
        if (platform === "ios"){
            const iosUIView = view.ios;
            // iosUIView.layer.shadowColor = UIColor.blackColor.CGColor;
            iosUIView.layer.shadowColor = new Color("black").ios.CGColor;
            iosUIView.layer.shadowOpacity = .25;
            iosUIView.layer.shadowOffset = CGSizeMake(5,5);
            iosUIView.layer.shadowRadius = 10;
            // iosUIView.layer.shadowPath = UIBezierPath.bezierPathWithRect(CGRectMake(1,1,200,200)).CGPath;
            //console.log(iosUIView);
        }
    }

</script>

<style>
    @keyframes ripple{
    from {
        transform: scale(0);
        opacity: 1;
    }
    to{
      transform: scale(20);
      opacity: 0;
    }
   }
    .circle{

        animation-name: ripple;
        animation-duration: 0.3;
        animation-timing-function: ease-in;

        background-color: rgba(255, 255, 255, 0.4);
        min-height: 20;
        min-width: 20;
        border-radius: 50;
        
        
        
        transform: scale(0);
        z-index: 99;
        position: absolute;
        
  }
  .circle-primary{

        animation-name: ripple;
        animation-duration: 0.3;
        animation-timing-function: ease-in;

        background-color: rgba(3, 110, 182, 0.4);
        min-height: 20;
        min-width: 20;
        border-radius: 50;
        
        
        
        transform: scale(0);
        z-index: 99;
        position: absolute;
        
  }
  .circle-secondary{

        animation-name: ripple;
        animation-duration: 0.3;
        animation-timing-function: ease-in;

        background-color: rgba(22, 193, 236, 0.4);
        min-height: 20;
        min-width: 20;
        border-radius: 50;
        
        
        
        transform: scale(0);
        z-index: 99;
        position: absolute;
        
  }
  .circle-purple{

        animation-name: ripple;
        animation-duration: 0.3;
        animation-timing-function: ease-in;

        background-color: rgba(155, 22, 243, 0.4);
        min-height: 20;
        min-width: 20;
        border-radius: 50;
        
        
        
        transform: scale(0);
        z-index: 99;
        position: absolute;
        
  }

    .rounded-light{
        border-radius: 5;
    }

    .rounded-heavy{
        border-radius: 50; 
    }
    .xlbtn{
        height: 80;
        width: 240;
    }
    .lgbtn{
        height: 60;
        width: 200;
    }
    .mdbtn{
        height: 50;
        width: 170;
    }
    .smbtn{
        height: 40;
        width: 150;
    }
    .lgfab{
        height: 80;
        width: 80;
    }
    .smfab{
        height: 60;
        width: 60;
    }

</style>

<!--fab-->

{#if iconString}
    <stackLayout id="button" on:loaded={onLoaded} >
        <stackLayout on:tap={onTouch} androidElevation="{androidShadowClass}" class="{fab_class_template}">
        <!-- <image src="{`font://&#x${iconString};`}" class="fas fa-comment" /> -->
        
            <image   top="-{circle_top}"
                left="{circle_left}"
                src="font://&#xf075;" class="fas t-36 z-50 absolute" />
        <absoluteLayout>
            <label bind:this={circle} id="circle" 
                class="{circleClass}" 
                text="" 
                top="-{circle_top}"
                left="{circle_left}"
            />
        </absoluteLayout>
            

        
        </stackLayout>
    </stackLayout>
    

    
       
{:else}

<!-- IOS -->

{#if (platform === "ios")}
<stackLayout on:loaded="{onLoaded}">
    <absoluteLayout id="button"  bind:this={wrapper} 
    class="{wrapper_class_template}" 
    horizontalAlignment="center" >

    
        <button on:tap={onTouch} class="{button_class_template}">
            {btnText}
    
        </button>
    
    
        <label bind:this={circle} id="circle" 
            class="{circleClass}" 
            text="" 
            top="{circle_top}"
            left="{circle_left}"
        />
    
    </absoluteLayout>
</stackLayout>



<!-- Android -->
{:else}

    
    
<stackLayout on:loaded={onLoaded} id={"button"}>

    <button
        horizontalAlignment="center" 
        on:tap={onTouch}
        class="{android_button_template}"
        androidElevation="{androidShadowClass}"
        >
            {btnText}
        </button>
</stackLayout>
    
    

    

{/if}

{/if}