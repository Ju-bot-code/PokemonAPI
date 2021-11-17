<script context="module">
  export async function load({page}){

    const url =`https://pokeapi.co/api/v2/pokemon?limit=150`
    const res =await fetch(url);
    const stuff =await res.json();

     const loadedPokemon=stuff.results.map((data,index)=>{
      return {
          name:data.name,
          id:index+1,
          image:`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`
    }
    })
    return {props :{Pokemon : loadedPokemon}}

  }

</script>

<script>
export let Pokemon;
import { paginate, LightPaginationNav } from 'svelte-paginate'
import { flip } from 'svelte/animate';
 
 let items = [... Pokemon];
 let currentPage = 1;
 let pageSize = 9;
 $: paginatedItems = paginate({ items, pageSize, currentPage })


//  import {Pokemon} from '../stores/mart';


//  console.log($Pokemon);
//  console.log(Pokemon);
 
 let searchTerm ='';

 $:{
    if(searchTerm){

        paginatedItems = Pokemon.filter(element=> element.name.toLowerCase().includes(searchTerm.toLowerCase()));
        items=[...paginatedItems]
    }else{
         items = [... Pokemon]
         paginatedItems;
     
    }
  }
 
  // console.log(Pokemon);
  let sort=false; 
  let Des=()=> {
    if(!sort){
      items = [... Pokemon.reverse()]
      sort=true;
    }

  }
  let Asc=()=> {
    if(sort){
      items = [... Pokemon.reverse()]
      sort=false; 
    }
  }

 
  // const months = ['March', 'Jan', 'Feb', 'Dec'];
  // months.sort();
  // console.log(months);
 



</script>


<!-- adds title to the page -->

<svelte:head>
  <title>Pokemon</title>  
</svelte:head>

<!-- <div class="my-10 mx-20 "> -->

    <h1 class="text-center text-xl font-thin uppercase text-gray-700 text-shadow">Svelte kit pokedex</h1>
    <div class="flex justify-center mt-2">
        <input type="text" bind:value={searchTerm} class="w-1/2 flex justify-center text-shadow-place border p-2 shadow-2xl placeholder-shown:uppercase font-thin placeholder-gray-400  " placeholder="Search Pokemon" >
       
        <div class="flex gap-x-4 mx-3 ">

          <button class="flex border shadow-2xl py-2 px-1 " on:click={Asc}>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-700 block " fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 11l7-7 7 7M5 19l7-7 7 7" />
            </svg>
          </button>

          <button class="flex border shadow-2xl py-2 px-1" on:click={Des}>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-700 block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 13l-7 7-7-7m14-8l-7 7-7-7" />
            </svg>
          </button>

        </div>

    </div> 
    {#if paginatedItems.length}
    <div  class="grid grid-cols-3  py-20 gap-y-10">
        {#each paginatedItems as pokeman (pokeman.id)}
          <div 	animate:flip="{{duration: 200}}" class="border shadow-xl p-1 rounded-md mx-10">
            <a href={`/poke/${pokeman.id}`} alt={pokeman.name}>
              <div class="border hover:bg-gray-100 rounded-md shadow-inner py-10 flex  flex-col items-center text-gray-900 ">
                
                <img src="{pokeman.image}" class="w-40 h-40 border rounded-md" alt="">
                <p class="flex uppercase mt-2 font-thin">{pokeman.id} ] {pokeman.name}</p>

              </div>  
            </a>
          </div>  
        {/each}
    </div>  
     {:else}
     <h3 class="flex justify-center text-gray-500 my-10 text-shadow-place">no results found</h3>
     {/if}
    <!-- <div class="shadow-inner"> -->
    <LightPaginationNav
     totalItems="{items.length}"
    pageSize="{pageSize}"
    currentPage="{currentPage}"
    limit="{1}"
    showStepOptions="{true}"
    on:setPage="{(e) => currentPage = e.detail.page}"
    />
  <!-- </div> -->

<!-- </div> -->

<style>
  /* @layer components{  */
   /* @responsive {  */
        .text-shadow {
          text-shadow: 0 5px 4px rgb(128, 123, 123);
        }
        .text-shadow-place {
          text-shadow: 0 0.9px 0px rgb(128, 123, 123);
        }
      
        .text-shadow-md {
          text-shadow: 0 4px 8px rgb(29, 3, 3), 0 2px 4px rgb(12, 8, 8);
        }
      
        .text-shadow-lg {
          text-shadow: 0 15px 30px rgb(29, 3, 3), 0 5px 15px rgb(44, 37, 37);
        }
      
        .text-shadow-none {
          text-shadow: none;
        }
       /* } 
 }  */
</style>