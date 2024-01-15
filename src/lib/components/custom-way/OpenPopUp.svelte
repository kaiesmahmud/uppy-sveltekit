<script>
	import FileUpload from '../FileUpload.svelte';
    import UppyFacebook from '../UppyFacebook.svelte';
    import UppyGoogleDrive from '../UppyGoogleDrive.svelte';
    import UppyInstagram from '../UppyInstagram.svelte';
    import UppyDropbox from '../UppyDropbox.svelte';
    import UppyGooglePhotos from '../UppyGooglePhotos.svelte';
    import UppyUnsplash from '../UppyUnsplash.svelte';
    import UppyUrl from '../UppyURL.svelte';
    export let openUppyPopUp ;

    import Uppy from '@uppy/core';
    import Dashboard from '@uppy/dashboard';
    import Tus from "@uppy/tus";
    import AwsS3 from "@uppy/aws-s3";
    import AwsS3Multipart from "@uppy/aws-s3-multipart";
    import XHRUpload from "@uppy/xhr-upload";
    import ImageEditor from "@uppy/image-editor";
    import DropTarget from "@uppy/drop-target";
    import Audio from "@uppy/audio";
    import Compressor from "@uppy/compressor";
    import FileInput from '@uppy/file-input';


    import '@uppy/core/dist/style.min.css';
    import '@uppy/file-input/dist/style.css';
    import { onMount } from 'svelte';
    
    onMount(()=>{
        new Uppy()
        .use(Dashboard, 
            { 
                // inline: true, 
                target: '#UppyInterFace' 
            }
        ).use(FileInput, 
            { 
                target: Dashboard, 
            }
        );
    })
</script>
<div class={` w-full ${openUppyPopUp?'flex':"hidden"} items-center justify-center  backdrop-blur-lg p-3`}>
    <div id="UppyInterFace" class="w-[80%] p-5 bg-blue-800 rounded">
          <div class={`${ openUppyPopUp === "uploadFiles" ? "inline-block ": "hidden"}`}>
               <FileUpload/>
          </div>
          <div class={`${ openUppyPopUp === "facebookUpload" ? "inline-block ": "hidden"}`}>
               <UppyFacebook/>
          </div>
          <div class={`${ openUppyPopUp === "gdrive" ? "inline-block ": "hidden"}`}>
               <UppyGoogleDrive/>
          </div>
          <div class={`${ openUppyPopUp === "instagramUpload" ? "inline-block ": "hidden"}`}>
               <UppyInstagram/>
          </div>
          <div class={`${ openUppyPopUp === "dropboxUpload" ? "inline-block ": "hidden"}`}>
               <UppyDropbox/>
          </div>
          <div class={`${ openUppyPopUp === "gPhotosUpload" ? "inline-block ": "hidden"}`}>
               <UppyGooglePhotos/>
          </div>
          <div class={`${ openUppyPopUp === "unplashUpload" ? "inline-block ": "hidden"}`}>
               <UppyUnsplash/>
          </div>
          <div class={`${ openUppyPopUp === "urlUpload" ? "inline-block ": "hidden"}`}>
               <UppyUrl/>
          </div>
     </div>
</div>
