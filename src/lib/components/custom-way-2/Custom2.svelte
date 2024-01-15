<script>
    import Icon from '@iconify/svelte';
    $: showUppy = false 
    const handleShowUppy = ()=> showUppy = !showUppy
    import Uppy from '@uppy/core';
    import Dashboard from '@uppy/dashboard';
    import RemoteSources from '@uppy/remote-sources';
    
    import '@uppy/core/dist/style.css';
	import '@uppy/dashboard/dist/style.css';
    import "./custom2.css"

    import { onMount } from 'svelte';
    let uppy 
    onMount(()=>{
        uppy = new Uppy()
        .use(Dashboard, { inline: true, target: '#UppyMain' })
        .use(RemoteSources, {
             companionUrl: "http://companion.uppy.io" ,
             sources: [ 'GoogleDrive','Dropbox', 'OneDrive' ,'Facebook', 'Instagram'] ,
            }
        )
        
    })
</script>
<div class="w-full   text-white backdrop-blur">
    <div class="w-full md:w-1/4 h-screen bg-slate-900">
        <div class="flex items-center gap-3">
            <div class="w-full p-5 bg-gray-700">upload files</div>
            <button on:click={handleShowUppy} class="p-5 text-2xl bg-gray-700">
                <Icon icon="tabler:dots" />
            </button>
        </div>
        
        <div id="UppyMain" class={`${showUppy? " block showList":" hidden hideList "} relative`}>hello</div>
        <div>
            hello
        </div>
    </div>
</div>