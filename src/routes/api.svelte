<script>

    //Post
    let firstName;
    let lastName;
    let age;
    let place;
    let remote=false;
    let skills =[];
    let designation=[];
    let results

    async function formSubmit()
    {   
        const res = await fetch('https://httpbin.org/post',{
            method:'POST',
            body:JSON.stringify({
                firstName,
                lastName,
                age,
                place,
                remote,
                skills,
                designation
            })
         })
         const data= await res.json();  
         results=JSON.stringify(data); 
    }


    //GET /posts/1

    let data='';
    let post='';

    async function getData()
    {
        const res = await fetch('https://jsonplaceholder.typicode.com/posts/1');
        const data=await res.json();
        post=JSON.parse(JSON.stringify(data));
        // console.log(data);
    }
    getData();

    //PUT 	/posts/1 

    let title='';
    let body='';
    let row='';
    

    async function putData(){
        const res =await fetch('https://jsonplaceholder.typicode.com/posts/1',
        {
            method:'PUT',
            body:JSON.stringify({
                id:post.id,
                userId:post.userId,
                title:title,
                body:body
            }),
            headers:{
                'Content-type':'application/json; charset=UTF-8',
            },
        })
        .then(response => response.json())
        .then( json => {
            row=json; 
        } )
    }

    //PATCH post
    let patchTitle='';
    let row1='';

    async function patchData(){
        const res =await fetch('https://jsonplaceholder.typicode.com/posts/1',{
            method:'PATCH',
            body:JSON.stringify({
                title: patchTitle,
            }),
            headers:{
                'Content-type': 'application/json; charset=UTF-8',
            }
           
        })

        .then(response => response.json())
            .then(data => row1=data)
    }

     //delete post


    let data3;
    let fetchedid;
    let fetId;

    let  fetchid=(id)=>{
        fetchedid=id;
    }

     async function deletePost(){
        const res =await fetch(`https://jsonplaceholder.typicode.com/posts/${fetchedid}`,{
            method:'Delete'
        })
        .then(response => response.json())
            .then(data =>{ 
            data3=data;
            fetId=fetchedid;
            })

            
     }


</script>

<div class="max-w-2xl mx-auto">
    <div class="p-4 border rounded-md">
            <h1 class="text-center text-xl my-4 font-thin uppercase text-gray-700 text-shadow">API POST</h1>
            <form on:submit|preventDefault={formSubmit} 
                class="flex flex-col space-y-3">
                <label for="firstname"> First Name</label>
                <input type="text" class="p-2 border rounded-md"
                            bind:value={firstName} 
                            placeholder="First Name"
                            >

                <label for="firstname"> Last Name</label>

                <input type="text" class="p-2 border rounded-md"
                            bind:value={lastName} 
                            placeholder="Last Name"
                            >

                <label for="firstname">Age</label>

                <input type="number" class="p-2 border rounded-md"
                            bind:value={age} 
                            placeholder="Age"
                            >
            
                <label for="firstname"> Place</label>

                <input type="text" class="p-2 border rounded-md"
                            bind:value={place} 
                            placeholder="Place"
                            >  

                <div class="flex">
                    <input class="mx-3" type="checkbox" bind:checked={remote}> remote
                </div>

                <div class="">
                    <h1>skill list</h1>
                    <input type="checkbox" class="mx-3" bind:group={skills} value="html"> html
                    <input type="checkbox" class="mx-4" bind:group={skills} value="css"> css
                    <input type="checkbox" class="mx-4" bind:group={skills} value="javaScript"> js
                </div>
                    
                <select name="designation" id="" multiple bind:value={designation}>
                        <option value="junior">junior</option>
                        <option value="mid-level">mid-level</option>
                        <option value="senior">senior</option>
                </select>
                
                <button class="p-3 bg-red-400 rounded-md">submit</button>
            </form>            

            <div class=" my-20 p-4 m-4 border rounded-md">
            <!-- <pre class="flex flex-wrap"> -->
                {results}
            <!-- </pre>  -->
            
            </div>
    </div>

    <div class=" my-20 p-4  border rounded-md">
        <h1 class="text-center text-xl my-4 font-thin uppercase text-gray-700 text-shadow">API GET</h1>
        <!-- <pre class="flex flex-wrap"> -->
            <!-- {#each data as  da}
             <p> {da.title}</p>   
            {/each} -->
        
        <p> <span class="underline">  id: </span>{post.id}</p> 
        <p> <span class="underline"> title:</span> {post.title}</p> 
        <p> <span class="underline"> body:</span> {post.body}</p> 
         
         
        <!-- </pre>  -->
     
     </div>


     <div class=" my-20 p-4  border rounded-md">
        <h1 class="text-center text-xl my-4 font-thin uppercase text-gray-700 text-shadow">API PUT</h1>
        
        <form on:submit|preventDefault={putData}  class="flex flex-col space-y-3 w-full">
            
                <label for="firstname"> title</label>
                <input class="p-2 border rounded-md"
                type="text" bind:value={title}> 

                <label for="firstname"> body</label>
                <textarea  class="p-2 border rounded-md"
                bind:value={body} /> 
  
            <button class="p-3 bg-red-400 rounded-md">submit</button>
        </form>

        <div class="p-2 space-y-3">
            <!-- <p> <span class="underline">  id: </span>{post.id}</p>  -->
            <p> <span class="underline"> title:</span> {row.title}</p> 
            <p> <span class="underline"> body:</span> {row.body}</p>
        </div>
        
     
     </div>


     <div class=" my-20 p-4  border rounded-md">
        <h1 class="text-center text-xl my-4 font-thin uppercase text-gray-700 text-shadow">API PATCH</h1>
        
        <form on:submit|preventDefault={patchData}  class="flex flex-col space-y-3 w-full">
            
                <label for="firstname"> title</label>
                <input class="p-2 border rounded-md"
                type="text" bind:value={patchTitle}> 

                 
  
            <button class="p-3 bg-red-400 rounded-md">submit</button>
        </form>

        <div class="p-2 space-y-3">
            <!-- <p> <span class="underline">  id: </span>{post.id}</p>  -->
            <p> <span class="underline"> title:</span> {row1.title}</p> 
            <!-- <p> <span class="underline"> body:</span> {row.body}</p> -->
        </div>
        
     
     </div>

     <div class=" my-20 p-4  border rounded-md">
        <h1 class="text-center text-xl my-4 font-thin uppercase text-gray-700 text-shadow">API DELETE</h1>
        
        <form on:submit|preventDefault={deletePost}  class="flex flex-col space-y-3 w-full">
            
            <button class="p-3 bg-red-400 rounded-md" on:click={()=>fetchid(1)}>submit</button>
            <button class="p-3 bg-red-400 rounded-md" on:click={()=>fetchid(2)}>submit</button>
            <button class="p-3 bg-red-400 rounded-md" on:click={()=>fetchid(3)}>submit</button>
        </form>

        {#if fetId}
            <p class="my-4">id:{fetId} deleted</p> 
        {/if}
    
        
     
     </div>
</div>

