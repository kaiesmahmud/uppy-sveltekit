<script>
  import Uppy from '@uppy/core';
  import {Dashboard} from '@uppy/svelte';
  import Tus from '@uppy/tus'; // Example of importing a plugin
  import XHRUpload from '@uppy/xhr-upload'; // Example of another plugin
    import { onMount } from 'svelte';

  let uppy;
    
  onMount(async () => {
    uppy = new Uppy({
      plugins: [
        Dashboard,
        Tus, // Add plugins as needed
        XHRUpload,
        // ...other plugins
      ],
      debug: true, // Enable debug logging for troubleshooting
      // Configure Uppy options
      uppyDashboard: {
        inline: true,
        target: "#uppy", // Mount to this element within the component
        showProgressDetails: true,
        proudlyDisplayPoweredByUppy: true
      },
      // Configure other plugins as needed
    });
    console.log(uppy)
    uppy.on('upload-success', (file) => {
      // Handle successful upload (e.g., send a request to your server)
      console.log('Upload successful:', file);
    });

    uppy.mount('#uppy');
  });
</script>




<h1 class="text-center font-bold text-3xl p-5">Uppy with SvelteKit</h1>

<div id="uppy"></div>

<style>
  @import '@uppy/core/dist/style.css';
  @import '@uppy/dashboard/dist/style.css';
  /* Import styles for other plugins as needed */
</style>