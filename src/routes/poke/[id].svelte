<script context="module">
    export async function load({page}){
        const id=page.params.id;
        const url=`https://pokeapi.co/api/v2/pokemon/${id}`;
        const res=await fetch(url);
        const data=await res.json();
        return {props:{data,id}};
    }
</script>
<script>
    export let data;
    export let id;
    //  let fetch =[... data.moves];
    //  console.log(fetch.indexOf(2));
    // const prev=()=>{
    //  id++;
    // }
</script>
<div class="mx-20 flex  justify-center text-gray-800">
    
   
   
  <!-- <button on:click={prev} class="mx-10">hy</button> -->

    <!-- <hr class="border-2 w-full"> -->
    <div class=" border p-10 shadow-2xl rounded-sm">
        <h1 class="text-center text-2xl font-thin uppercase "> {data.name}</h1>
        <div class="flex">
            <img class="w-40 h-40" src={`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${id}.png`} alt={data.name}>
            <img  class="w-40 h-40" src={`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/${id}.png`} alt={data.name}>
        </div>

      

        <div class="flex gap-32">
            <div class="">
                <div class="flex flex-col   font-thin mb-5">
                    <h3><span class="uppercase">HEIGHT :</span> {data.height} feet</h3>
                    <h3><span class="uppercase">WEIGHT :</span> {data.weight} kgs</h3>
                </div>
                <h2 class=" text-2xl font-thin uppercase  ">Abilities</h2>
                <div class="mt-2">
                    {#each data.abilities as dat ,i }
                    
                    <h3 class="font-thin text-gray-900 ">{i}] {dat.ability.name}</h3> 
                    {/each}
                </div>    
            </div>

            <div>
                <h2 class="text-center text-2xl font-thin uppercase">TOP 5 MOVES</h2>
                <div class="mt-2 ">
                    {#each data.moves as mo ,i}
                    {#if i < 5}
                        <h3 class="font-thin text-gray-900">{i+1}] {mo.move.name}</h3>
                    {/if}
                    {/each}
                </div>
            </div>
        </div>
    </div> 
    <!-- <button class="mx-10">hy</button>   -->

   
    
</div>