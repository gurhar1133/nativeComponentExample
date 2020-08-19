<script>
    import { Template } from 'svelte-native/components';
    import { onMount } from 'svelte';
    import {Color} from "color";
    import Button from "./Button.svelte";
    import Card from "./Card.svelte";
    import Overlay from "./Overlay.svelte";
    import Textfield from "./Textfield.svelte";
    import Grid from "./Grid.svelte";
    import { showModal } from 'svelte-native';
    import { navigate } from 'svelte-native';
    import { closeModal } from 'svelte-native';
    const platformModule = require("tns-core-modules/platform");

    let selectedTab;
    let message = "Svelte-Native Components Practice!";
    let label;
    let instructions = [
        {name: "1) Make components"},
        {name: "2) Refer to Veutify for the components design"},
        {name: "3) For this project (but not the web version), it is ok to alter App.svelte if you need to, just dont alter component calls "},
        {name: "4) See repo for instructions for icons"},
        {name: "5) Use tailwind, or vanilla css, whatever works"},
        {name: "6) Tabstrip instructions: Visit this link \nhttps://icons8.com/articles/ui-inspiration-tab-bar-animations/ \n to get inspiration to customize the tabstrip as you like (dont have to obsess over super fancy animation. Something nice and simple will suffice)."},
        {name: "7) Contact me with any issues"}
    ];
    let overlay1 = false;
    let overlay2 = false;
    let overlay;
    let platform;
    let plat = platformModule.isIOS ? "ios" : "android";
    // useful for centering elements that are wrapped in absolute layout
    //let screenWidth = platformModule.screen.mainScreen.widthPixels;
    //console.log("Screen Width: ", screenWidth, typeof screenWidth);
    let rotationClass1;

    let rotationClass2;

    let wrap1;
    let wrap2;
    let tab1;
    let tab2;
    let selected1;
    let selected2;

    let androidAnimationClass1;
    let androidAnimationClass2;
    
    let overlayData = {
        type: "Card", props:{
          title: "Card Test2", 
          subtitle: "Test", 
          description: "Lorem ipsum blah blah blah",
          hasImage: true,
          imgSrc: "https://www.lysergic.net/wp-content/uploads/2017/07/figure_grid_dimple_dylan_bakker-750x1000.jpg",
          shaped: true
         }
    }
    // let modalResult = "Waiting for modal"
	// async function launchModal() {
    //     console.log("launching the modal");
    //     // you can pass a component into the show modal call
    //     let result = await showModal({page: Overlay, props: { value: true, absolute: false, modalMessage: "close"}})
	// 	// modalResult = `got result: ${result}`
    // }
    
    
    function onLoaded(args){
        let page = args.object;
        tab1 = page.getViewById("tab1");
        tab2 = page.getViewById("tab2");
        wrap1 = page.getViewById("wrap1");
        wrap2 = page.getViewById("wrap2");
        // console.log("page: ",page);
    }

    function rotateTab(args){
        // console.log(args.object.id);
        
        if (args.object.id === "tab1"){
        //    console.log(tab1)
            selected1 = "selected-icon";
            selected2 = "";
            if (plat === "ios"){
                const iosUIView = wrap1.ios;
                // iosUIView.layer.shadowColor = UIColor.blackColor.CGColor;
                iosUIView.layer.shadowColor = new Color("black").ios.CGColor;
                iosUIView.layer.shadowOpacity = .5;
                iosUIView.layer.shadowOffset = CGSizeMake(5,5);
                iosUIView.layer.shadowRadius = 10;
                // iosUIView.layer.shadowPath = UIBezierPath.bezierPathWithRect(CGRectMake(1,1,200,200)).CGPath;
                // console.log(iosUIView);
                const iosUIView2 = wrap2.ios;
                // iosUIView.layer.shadowColor = UIColor.blackColor.CGColor;
                iosUIView2.layer.shadowColor = new Color("black").ios.CGColor;
                iosUIView2.layer.shadowOpacity = .0;
                iosUIView2.layer.shadowOffset = CGSizeMake(5,5);
                iosUIView2.layer.shadowRadius = 10;
                tab1.animate({
                    scale: {x: 1.5, y: 1.5},
                    duration: 500,
                    rotate: 360
           
                });
                tab2.animate({
                    scale: {x: 1, y: 1}
                });
            } 
            else if (plat === "android"){
                androidAnimationClass1 = "spin expand";
                setTimeout(()=>{
                    androidAnimationClass1 = "";
                }, 500)
            }
        
           
            selectedTab = 0;
        }
        else if (args.object.id=== "tab2"){
            // rotationClass2 = "animated";
            // rotationClass1 = ""
            // console.log(tab2);
            if (plat === "ios"){
                const iosUIView = wrap2.ios;
                // iosUIView.layer.shadowColor = UIColor.blackColor.CGColor;
                iosUIView.layer.shadowColor = new Color("black").ios.CGColor;
                iosUIView.layer.shadowOpacity = .5;
                iosUIView.layer.shadowOffset = CGSizeMake(5,5);
                iosUIView.layer.shadowRadius = 10;
                // iosUIView.layer.shadowPath = UIBezierPath.bezierPathWithRect(CGRectMake(1,1,200,200)).CGPath;
                //console.log(iosUIView);
                const iosUIView2 = wrap1.ios;
                // iosUIView.layer.shadowColor = UIColor.blackColor.CGColor;
                iosUIView2.layer.shadowColor = new Color("black").ios.CGColor;
                iosUIView2.layer.shadowOpacity = .0;
                iosUIView2.layer.shadowOffset = CGSizeMake(5,5);
                iosUIView2.layer.shadowRadius = 10;
                tab2.animate({
                    scale: {x: 1.5, y: 1.5},
                    duration: 500,
                    rotate: 360
                });
                tab1.animate({
                    scale: {x: 1, y: 1}
                });
                
            }
            else if (plat === "android"){
                androidAnimationClass2 = "spin expand";
                setTimeout(()=>{
                    androidAnimationClass2 = "";
                }, 500)
            }
            selected2 = "selected-icon";
            selected1 = "";
            
            selectedTab = 1;
        }
        // console.log("rotation classes: ", rotationClass1, rotationClass2);
    }
    $: gridItems = [
      {
        type: "Card", props: {
          title: "Card Test", 
          subtitle: "Test", 
          description: "Lorem ipsum blah blah blah",
          hasImage: true,
          imgSrc: "https://www.pngkey.com/png/detail/767-7671067_minecraft-pixel-art-grid.png",
          shaped: true
         
        }
        
      },
      {
        type: "Card", props:{
          title: "Card Test2", 
          subtitle: "Test", 
          description: "Lorem ipsum blah blah blah",
          hasImage: true,
          imgSrc: "https://www.lysergic.net/wp-content/uploads/2017/07/figure_grid_dimple_dylan_bakker-750x1000.jpg",
          shaped: true
         }
        
      },
      {
        type: "Card", 
        props: {
          title: "Card Test3", 
          subtitle: "Test", 
          description: "Lorem ipsum blah blah blah",
          hasImage: true,
          imgSrc: "https://images.artistrunwebsite.com/arwblog/bg_37311453262250.jpg?1453262251",
          shaped: true
        }
        
      },
      {
        markup: "<h3 class='text-xl' style='color:red;'>Hello World</h3>"
      },
      {
        type: "Button",
        props: {
          btnText: "Click me!",
          elevation: "lg",
          rounded: true,
          textMode: true
        }
        
      }
      
    ];
  
</script>

<style>
   .bottom-icon{
       
       height: 50;
       width: 50;
       padding: 5 5 5 5;
       color: #fff;
       border-width: 1;
       border-color: transparent;
       
       
   }
   .selected-icon{
        /* animation: fillout-from-nothing 0.5s linear;
        
        border-width: 3;
        border-color: #fff; */
   }
   
   .spin {
        animation-name: rotate;
        animation-duration: .4s;
        
      
    }
    .expand{
        animation: fillout 0.5s ease;
    }

   @keyframes fillout{
   
    to{
        transform: scale(1.3);
    }

    
}
@keyframes fillout-from-nothing{
   from {transform: scale(0);}
    to{
        transform: scale(1);
    }

    
}

@keyframes rotate {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

</style>


<page on:loaded={onLoaded}>
  
    <actionBar title="{message}" class="text-center bg-green-500 text-white px-2 py-4 flex">
        

    </actionBar>
    <gridLayout rows="7*, 1*">
     <tabStrip highlightColor="red"  selectedItemColor="#fff" class="bg-green-500 text-white" >
						<tabStripItem   horizontalAlignment="center">
                            
                            
                                <!-- <label>Instructions</label> -->
                                <!-- <image src="font://&#xf015;" id="" class="{`fas t-36`}" /> -->
                          
                            
                        </tabStripItem>
						<tabStripItem horizontalAlignment="center">
                            
                            
                                <!-- <label>Components</label> -->
                                <!-- <image src="font://&#xf085;" id="" class="{`fas fa-cogs`}" /> -->
                            
                            
						</tabStripItem>
						
	    </tabStrip>
    <tabs bind:selectedIndex={selectedTab} iOSTabBarItemsAlignment="centerSelected" tabsPosition="bottom">
       




        <tabContentItem>
            <stackLayout  class="relative">
                <label text="Instructions" class="text-center text-xl bg-green-500 text-white py-2 px-2" />
                    <listView class="h-full"  items="{instructions}" >
								<Template let:item>
									<label class="text-center" text="{item.name}" textWrap="true" />
								</Template>
			        </listView>
            </stackLayout>
        </tabContentItem>




        <tabContentItem>
        
            <scrollView row="0">
           
            <stackLayout class="z-10 bg-gray-100" row="1">
            
            <label text="Buttons" class="text-center text-xl bg-green-500 text-white  py-2 px-2 m-b-4" />
               
                    <!--
                        Buttons go here
                    -->
                    
                <Button 
                    
                    btnText="Large Primary"
                    color="primary"
                    size="xl"
                    elevation="sm"
                    on:tap={()=>{
                        //console.log("tap tap");
                    }}
                /> 

            <!-- Buttons can have different levels of elevation -->

                <Button 
                   
                    btnText="Block Secondary Raised High"
                    color="secondary"
                    size="block"
                    elevation="lg"
                />

                <!--default color should be purple like vuetify buttons
                        default size is md-->

                <Button
                    
                    btnText="Rounded"
                    size="lg"
                    rounded={true} /> 

            
                <Button 
                    
                    btnText="Outline"
                    outline={true}
                    elevation={"none"} />

                <Button 
                       
                        btnText="Outline"
                        outline={true}
                        elevation={"none"}
                        color="primary" />
                <Button 
                    
                    btnText="Text Button"
                    textMode={true} 
                    elevation={"none"}/>  

            <!-- by default disabled is false. Buttons should be disableable-->
 
                <Button
                    
                    btnText="Disabled"
                    disabled={true} />

                <!-- put font awesome comment icon in this button. No btnText-->

                <Button fab={true} 
                        elevation="lg"
                        iconString="f075"/>
                        
                <Button fab={true} 
                        elevation="sm"
                        size="lg"
                        iconString="f075"/> 
                    
                   
            <label text="Cards" class="text-center text-xl bg-green-500 text-white  py-2 px-2 my-4"  />
                <!--
                        Cards go here
                -->
                <Card title="Vegeta"
                        platform="{platform}"
                        subtitle="Prince of Sayans"
                        description="Lorem ipsum ....."
                        hasImage={true}
                        imgSrc="https://qph.fs.quoracdn.net/main-qimg-40ccab97c4b182082c3525bb34575a37.webp"
                        elevation="lg"
                    >
        
                    </Card>

                <Card title="Svelte"
                        platform="{platform}"
                        subtitle="Javascript Framework"
                        description="Lorem ipsum ....."
                        hasImage={true}
                        imgSrc="https://i0.wp.com/programmingwithmosh.com/wp-content/uploads/2019/12/1_OJLglSTFZ1PbwpRG0U2xXA.png?ssl=1"
                        elevation="sm"
                    >
        
                    </Card>

                <!-- nesting Button in Card -->

                <Card title="Card with buttons"
                            platform="{platform}"
                         subtitle="No Image"
                        >
                        <Button fab={true} 
                            elevation="lg"
                            iconString="font://&#xf015;"/>
                    </Card>
 
 
                    <Card title="Tailwind"
                            platform="{platform}"
                            subtitle="Design"
                            description="Lorem ipsum ....."
                            hasImage={true}
                            shaped={true}
                            imgSrc="https://pbs.twimg.com/profile_images/895274026783866881/E1G1nNb0.jpg"
                            elevation="lg"
                    >
        
                    </Card>


                <!-- Come up with your own bonus card attribute for this one.
                Doesnt have to fit the vuetify design pattern. Could be animation, styling, etc-->  

                    <Card title="Bonus"
                                platform="{platform}"
                                subtitle="Your own bonus property"
                                description="Lorem ipsum ....."
                                hasImage={true}
                                shaped={true}
                                imgSrc="https://www.travelweek.ca/wp-content/uploads/2020/04/Travel-Edge-investing-50-million-in-signing-bonus-incentive-for-luxury-travel-advisors.jpg"
                                bonus={true}
                                >
        
                            </Card>
            


            
           <label text="Overlays" class="text-center text-xl bg-green-500 text-white  py-2 px-2 m-b-4" />
                
                
                <absoluteLayout height="300">
                    
                        <Button 
                            platform="{platform}"
                            btnText="abs Overlay"
                            color="primary"
                            size="xl"
                            elevation="sm"
                            on:tap={()=>{overlay1 = !overlay1}}
                            /> 
                   
                    
                    <Overlay 
                            absolute="{true}" 
                            platform="{platform}"
                            opacity="{.5}" 
                            zIndex="{99}" 
                            bind:value="{overlay1}" 
                            > 
                            <Button 
                            platform="{platform}"
                            btnText="Hide Overlay"
                            color="primary"
                            size="xl"
                            elevation="sm"
                            on:tap={()=>{overlay1 = !overlay1}}
                            />  
                    </Overlay>
                   
                </absoluteLayout>
                 

                     <Button     
                            platform="{platform}"
                            btnText="full overlay"
                            color="primary"
                            size="xl"
                            elevation="sm"
                            on:tap={()=>{overlay2 = !overlay2}}
                        /> 
                
                <Overlay 
                            absolute="{false}" 
                            platform="{platform}"
                            opacity="{.5}" 
                            zIndex="{99}" 
                            component="{overlayData}"
                            bind:value="{overlay2}" 
                            > 
                            <Button 
                            platform="{platform}"
                            btnText="Hide Overlay"
                            color="primary"
                            size="xl"
                            elevation="sm"
                            on:tap={()=>{overlay2 = !overlay2}}
                            />  
                    </Overlay> 
                
 
                
    
            <label text="Textfields" class="text-center text-xl bg-green-500 text-white  py-2 px-2 m-b-4" />
                <!-- A see Vuetify examples for this basic text input -->

                <Textfield on:return={()=>{
                    //console.log(event.detail);
                    }}
                     platform="{platform}" placeHolder="Default text input" />
                <Textfield on:return={()=>{
                    //console.log(event.detail);
                    }}
                    platform="{platform}" placeHolder="Filled" filled={true} />
               <Textfield on:return={()=>{
                    //console.log(event.detail);
                    }}
                     platform="{platform}" placeHolder="Oulined" outlined={true} />
        
                

            <label text="Grids" class="text-center text-xl bg-green-500 text-white  py-2 px-2 m-b-4" />
             <!-- This builds on the gridLayout component -->
             <label text="Default two column" class="text-center bg-green-500 text-white  py-2 px-2 m-b-4" />
            
                <Grid gridElements={gridItems} />

            <label text="One column" class="text-center bg-green-500 text-white  py-2 px-2 m-b-4" />
            
                <Grid gridElements={gridItems} numCols={1}/>

            <label text="Three column" class="text-center bg-green-500 text-white  py-2 px-2 m-b-4" />
            

                <Grid gridElements={gridItems} numCols={3}/>
                

                <stackLayout style="height: 150;">
                </stackLayout>
             </stackLayout>

            
        
        </scrollView>
        </tabContentItem>
        
            
            
        
        
                

    </tabs>
    <gridLayout androidElevation="24" row="1"  columns="*,*" class="text-center text-xl bg-green-500 text-white px-2">
            {#if plat === "ios"}
            <gridLayout  col="0" id="wrap1"  class="{`${selected1}`}">
               
                    <image  id="tab1" src="font://&#xf015;" on:tap={rotateTab} class="{`fas bottom-icon my-2 mx-2`}" />
               
            </gridLayout>
            
            
                <gridLayout  id="wrap2" col="1" class="{`${selected2}`}">
                
                    <image  id="tab2" src="font://&#xf085;" on:tap={rotateTab} class="{`fas fa-cogs bottom-icon my-2 mx-2`}" />
               
                
                </gridLayout>
            
            {:else if plat === "android"}
                <gridLayout col="0"  class="{`${selected1}`}">
                    <image id="tab1" src="font://&#xf015;" on:tap={rotateTab} class="{`fas bottom-icon ${androidAnimationClass1}`}" />
                
                </gridLayout >
                    
                <gridLayout col="1" class="{`${selected2}`}">
                    <image  id="tab2" src="font://&#xf085;" on:tap={rotateTab} class="{`fas fa-cogs bottom-icon ${androidAnimationClass2}`}" />
                
                </gridLayout>
                    
              
            {/if}
                </gridLayout>
        </gridLayout>

</page>



