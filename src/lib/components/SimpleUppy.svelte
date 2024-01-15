<script>
    import Uppy from '@uppy/core';
    import Dashboard from '@uppy/dashboard';
    import RemoteSources from '@uppy/remote-sources';

    // import '@uppy/core/dist/style.min.css';
    // import '@uppy/dashboard/dist/style.min.css';
    import { onMount } from 'svelte';
    //import './uppy-custom.css'; /* Import custom CSS */
    let uppy ,enableRemoteSource
    onMount(()=>{
        uppy = new Uppy()
        .use(Dashboard, { inline: true, target: '#uppy-dashboard' })
        .use(RemoteSources, {
             companionUrl: "http://companion.uppy.io" ,
             sources: ['Box', 'Dropbox', 'Facebook', 'GoogleDrive','Instagram', 'OneDrive', 'Unsplash', 'Url', 'Zoom'] ,
             providerOptions: {
                    Facebook: false, // Disable Facebook initially
                }
            }
        )
        
    })
    enableRemoteSource = (sourceName)=> {
        console.log(uppy)
        console.log(uppy.getPlugin("remote-sources"))
        // uppy.getPlugin("Facebook").setOptions({
        //     providerOptions: {
        //         [sourceName]: true, // Enable the specified source 
        //     }
        // });
        // uppy.open(); // Open the Dashboard to display the enabled source
    }
</script>
<div>
</div>
<div id="uppy-dashboard" >
    <!-- <button on:click={()=>{enableRemoteSource('Facebook')}} class="p-5 bg-blue-400 rounded ">Facebook</button> -->
    <!-- Basic -->
</div>