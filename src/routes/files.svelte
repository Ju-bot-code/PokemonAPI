<script>



    //file upload
    let files=[];



  //image upload
  let fileinput,placeHolder;

  const fileUpload=(e)=>{

       let image=e.target.files[0];

            let reader= new FileReader();

            reader.readAsDataURL(image);
            reader.onload = e =>{
                placeHolder=e.target.result
                // console.log('new',placeHolder);
            };

    //    console.log(image);

  }

  //multi image upload
//   function previewImages() {

//     var preview = document.querySelector('#preview');

//     if (this.files) {
//     [].forEach.call(this.files, readAndPreview);
//     }

//     function readAndPreview(file) {

//   // Make sure `file.name` matches our extensions criteria
//   if (!/\.(jpe?g|png|gif)$/i.test(file.name)) {
//     return alert(file.name + " is not an image");
//   } // else...
  
//   var reader = new FileReader();
  
//   reader.addEventListener("load", function() {
//     var image = new Image();
//     image.height = 100;
//     image.title  = file.name;
//     image.src    = this.result;
//     preview.appendChild(image);
//   });
  
//   reader.readAsDataURL(file);


  
// }

// }

// my try 

    let input ;
    let image=[] ;
    let more=[];
    let data=[];


    const  multipleupload = (e) =>{
        

        image=e.target.files;
        console.log( e.target.files.File)
        var preview = document.querySelector('#preview');
       
        
            [...image].forEach(element => {

                         e.target.files;

                        let reader = new FileReader();

                            reader.readAsDataURL(element) ;

                            reader.onload= e =>{
                                //  yes= e.target.result;
                                // more.push(yes);

                                var image = new Image();
                                // image.height = 100;
                                image.src =  e.target.result;
                                preview.appendChild(image);
                                more.push(image);
                                
                            }
                });
           
       
    }

 
 

	
</script>

<div class="p-20 border rounded-md">

    <h1>File upload</h1>

    <input type="file" bind:files> 
    {#if files && files[0]}
        <p>{files[0].name}</p>
    {/if}

</div>

<div  class="p-20 border my-2 rounded-md">

    <h1>Image upload</h1>
    
    <div class="flex gap-4">

        <div on:click={fileinput.click()}>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
            </svg>
        </div>
        
        {#if placeHolder}
        <img src={placeHolder} class="w-20 rounded-full h-20 my-2" alt="uploadedIamge">
        {/if}

    </div>
   




   <input type="file" class="hidden" accept=".jpeg,.png,.jpg" bind:this={fileinput} 
        on:change={(e)=>fileUpload(e)}>

</div>



<!-- <div  class="p-20 border my-2 rounded-md">
    <input on:change={previewImages} type="file" multiple accept=".jpeg,.png,jpg">
    <div id="preview" class="w-20 h-20 rounded-full my-2"></div>
</div> -->

<div>
    <h1>my try </h1>

    <input type="file" accept='.jpeg,.jpg,.png' multiple bind:this={input} on:change={(e)=> multipleupload(e)}>
    <div id="preview" class="w-20 h-20 rounded-full space-x-4 flex"></div>
    <!-- {#if multipleupload}
        {#each image  as mo }
            <img src={mo} alt="">
        {/each}
    {/if} -->
</div>

  
       
