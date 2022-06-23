

  <script>
      import { onMount } from 'svelte';
      // import Dropzone from  "svelte-file-dropzone";

      let Dropzone;

    onMount(async () => {
        const module = await import('svelte-file-dropzone');
        Dropzone = module.default;
    });
  
  
 

  let files = {
      accepted: [],
      rejected: []
    };
    let placeHolder;
    let images=[];
  


  function handleFilesSelect(e) {

    files = e.detail.acceptedFiles;
    var preview = document.querySelector('#preview');
    for (let i = 0; i < files.length; i++) {
      const reader = new FileReader();
      reader.readAsDataURL(files[i]);
      reader.onload = (e) => {
        var image = new Image();
          image.style.height="60px";
          image.style.width="60px";
          image.style.borderRadius="50px";
          image.style.border = "thin solid #ea8df2";
          image.src =  e.target.result;
          preview.appendChild(image);
          more.push(image);

      };


  }

}


  function handleRemoveFile(e, index) {
    files.accepted.splice(index, 1);
    files.accepted = [...files.accepted];
  }
  function handleRemoveAll() {
    files.accepted = [];
  }



  </script>


  
  <!-- <Dropzone  /> -->
  <svelte:component this={Dropzone} on:drop={handleFilesSelect} accept=".png,.jpeg,.jpg" muiltipe >
      <button class="border p-1 bg-gradient-to-r from-blue-400 text-white via-pink-400 to-purple-500 rounded-md">Choose images to upload</button>
      <p class="text-pink-400">or</p>
      <p class="text-pink-400">Drag and drop them here</p>
      <div class="w-full">

        <div id="preview" class=" rounded-full space-x-4 my-1 justify-center flex-wrap flex"></div>
      </div>
</svelte:component>
<div style="margin: 5px;">
  {#if files.accepted.length > 0}
    <button class="border p-1" on:click={handleRemoveAll}>RemoveAll</button>
  {/if}
  {#each files.accepted as item, index}
    <div class="gap-1">
      <span>{item.name}</span>
      {item.File}
      <img src="{item.path}" alt="{item.name}">
      <button on:click={e => handleRemoveFile(e, index)} class="border p-1">Remove</button>
    </div>
  {/each}
</div>

<style>
  .dropzone{
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    border-width: 2px;
    border-radius: 2px;
    border-color: #c03333;
    border-style: dashed;
    background-color: #fafafa;
    color: #bdbdbd;
    outline: none;
    transition: border 0.24s ease-in-out;
  }
</style>
<!-- </div> -->



