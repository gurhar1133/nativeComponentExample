<script>
    export let gridElements;
    export let numCols = 2;
    
    import Button from './Button.svelte';
    import Card from "./Card.svelte";
    import Overlay from "./Overlay.svelte";
    import Textfield from "./Textfield.svelte";

    let numRows = Math.round(gridElements.length / numCols);

    let rows = "";
    for (let i = 0; i < numRows; i++){
        if (i == numRows - 1){
            rows = rows + "1*";
        }
        else{
            rows = rows + "1*,";
        }
    }

    let cols = "";
    if (numCols === 1){
        cols = "*";
    }
    else
    {
        for (let i = 0; i < numCols; i++){
            if (i == numCols - 1){
                cols = cols + "1*";
            }
            else{
                cols = cols + "1*,";
            }
        }
    }
    
    
    
    // console.log("COLS: ", cols);
    // console.log("NUMROWS: ", numRows);
    // console.log("ROWS: ", rows);

    let components = {"Button": Button, "Textfield": Textfield, "Card": Card,
         "Overlay": Overlay};
    
    function indexTransform(index){
        //console.log("Col: ", index % numCols , "For index: ", index);
        return (index % numCols).toString(); 
    }

    function indexToRow(index){
        //console.log("ROW: ", Math.round(index/numCols), " For index: ",  index);
        return Math.floor(index/numCols).toString();
    }
</script>
<style>

</style>

<gridLayout columns="{cols}" rows="{rows}">
{#each gridElements as gridElem, index}
    
    <gridLayout col="{indexTransform(index)}" row="{indexToRow(index)}" >
    <!-- <label text={index.toString() + ", " + indexTransform(index) + ", " + indexToRow(index)} /> -->
    {#if gridElem.type === "Card"}

                <Card {...gridElem.props}>
                   <!-- {#if gridElem.props.slotContent}
                        <svelte:component this={components[gridElem.props.slotContent.type]} 
                            {...gridElem.props.slotContent.props}/>
                    {/if} -->
                </Card>

            {:else if gridElem.type === "Button"}

                <Button
                    {...gridElem.props}
                    />

            {:else if gridElem.type === "Textfield"}

                <Textfield {...gridElem.props} />

            {:else if gridElem.type === "Overlay"}
                
                <Overlay {...gridElem.props}>

                    <!-- {#if gridElem.props.slotContent}
                        <svelte:component this={components[gridElem.props.slotContent.type]} 
                            {...gridElem.props.slotContent.props}/>
                    {/if} -->

                </Overlay>
            <!-- {:else if gridElem.type === "Grid"}
                <svelte:self {...gridElem.props} /> -->
            {:else}
                <htmlView html={gridElem.markup} /> 
            {/if}
    </gridLayout>
{/each}

</gridLayout>