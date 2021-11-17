
<script>
    export let userName;
    export let id;
    export let i;
    export let jobTitile;
    export let url;
    export let description;
</script>
<div class="p-2 border shadow-lg my-10">
    <h1 class="my-2 text-xl">#{i +1 }</h1>
    <!-- <p>#{id}</p> -->
    <div class="flex border-b-2">
        <div>
            <img src="{url}"
             alt="{userName}" class="w-32 h-32"></div>
        <div class="mx-3 space-y-2">
            <h1 >{userName}</h1>
            <p>{jobTitile}</p>
        </div>
    </div>
    <div class="my-2">
       
        <p>{description}</p>
    </div>
</div>