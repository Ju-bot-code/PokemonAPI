<script>
    import Card from './card.svelte'
    let userName='';
    let jobTitile='';
    let url='';
    let description='';
    let cardStack=[];
    let validation;

    function addCard (){

        if(userName.trim().length !== 0 &&
           jobTitile.trim().length !== 0 &&
           url.trim().length !== 0 &&
           description.trim().length !== 0
            )
        {   
                 cardStack=[...cardStack , 
                        {userName , 
                        jobTitile,
                        url,
                        description ,
                        id: Math.random()}
                        ];
        } else{
          validation ='all fields are required';
        }

    }

    function deleteFirst()
    {
        cardStack=cardStack.slice(1);

    }

    function deleteLast()
    {
        cardStack=cardStack.slice(0,-1);
    }

    // $:console.log(userName.trim().length);

</script>




<svelte:head>
    <title>About Us</title>
</svelte:head>

<h1 class="text-center text-2xl font-thin">
    About page [NOTES]
</h1>
    <div class=" mx-auto max-w-2xl">
        <div class="flex flex-col my-4 space-y-3">

        <label for="UserName">User Name</label>
        <input class="border-2" type="text" bind:value={userName}>

        <label for="jobTitile">Job Titile</label>
        <input class="border-2" type="text" bind:value={jobTitile}>

        <label for="Image">Image</label>
        <input class="border-2" type="text" bind:value={url}>

        <label for="Description">Description</label>
        <textarea class="border-2" type="text" bind:value={description}/>

        <div>
            <button on:click={addCard} class="p-2 bg-pink-600 text-white">Add Card</button>
            <button on:click={deleteFirst} class="p-2 bg-pink-600 text-white">Delete First</button>
            <button on:click={deleteLast} class="p-2 bg-pink-600 text-white">Delete Last</button>

        </div>

        </div>
    
        {#each  cardStack as  card  ,i(card.id) }
           
            <Card userName={card.userName} {i}  id={card.id} jobTitile={card.jobTitile} url={card.url}  description={card.description}></Card>
        {:else}
            {#if validation}
            <p>   {validation}</p>
            {/if}
            <p>please fill the form </p>
        {/each}
    
    
    </div>














