<script>
	import Uppy, { debugLogger } from "@uppy/core";
  import Dashboard from "@uppy/dashboard";
  import RemoteSources from "@uppy/remote-sources";
  import Webcam from "@uppy/webcam";
  import ScreenCapture from "@uppy/screen-capture";
  import GoldenRetriever from "@uppy/golden-retriever";
  import Tus from "@uppy/tus";
  import AwsS3 from "@uppy/aws-s3";
  import AwsS3Multipart from "@uppy/aws-s3-multipart";
  import XHRUpload from "@uppy/xhr-upload";
  import ImageEditor from "@uppy/image-editor";
  import DropTarget from "@uppy/drop-target";
  import Audio from "@uppy/audio";
  import Compressor from "@uppy/compressor";

  import "@uppy/core/dist/style.css";
  import "@uppy/dashboard/dist/style.css";
  import "@uppy/audio/dist/style.css";
  import "@uppy/screen-capture/dist/style.css";
  import "@uppy/image-editor/dist/style.css";
  import { onMount } from "svelte";

const UPLOADER = "tus";
const COMPANION_URL = "http://companion.uppy.io";
const companionAllowedHosts = [];
const TUS_ENDPOINT = "https://tusd.tusdemo.net/files/";
const XHR_ENDPOINT = "";

const RESTORE = false;
let uppyDashboard ;
onMount(()=>{
    uppyDashboard = new Uppy({ logger: debugLogger })
      .use(Dashboard, {
        inline: true,
        target: "#app",
        showProgressDetails: true,
        proudlyDisplayPoweredByUppy: true
      })
      .use(RemoteSources, {
        companionUrl: COMPANION_URL,
        sources: [
          "Box",
          "Dropbox",
          "Facebook",
          "GoogleDrive",
          "Instagram",
          "OneDrive",
          "Unsplash",
          "Url"
        ],
        companionAllowedHosts
      })
      .use(Webcam, {
        target: Dashboard,
        showVideoSourceDropdown: true,
        showRecordingLength: true
      })
      .use(Audio, {
        target: Dashboard,
        // target: '#audio',
        showRecordingLength: true
      })
      .use(ScreenCapture, { target: Dashboard })
      .use(ImageEditor, { target: Dashboard })
      .use(DropTarget, {
        target: document.body
      })
      .use(Compressor);

      switch (UPLOADER) {
        case "tus":
          uppyDashboard.use(Tus, { endpoint: TUS_ENDPOINT, limit: 6 });
          break;
        case "s3":
          uppyDashboard.use(AwsS3, { companionUrl: COMPANION_URL, limit: 6 });
          break;
        case "s3-multipart":
          uppyDashboard.use(AwsS3Multipart, {
            companionUrl: COMPANION_URL,
            limit: 6
          });
          break;
        case "xhr":
          uppyDashboard.use(XHRUpload, {
            endpoint: XHR_ENDPOINT,
            limit: 6,
            bundle: true
          });
          break;
        default:
      }
      
      if (RESTORE) {
        uppyDashboard.use(GoldenRetriever, { serviceWorker: true });
      }
      
      window.uppy = uppyDashboard;
      
      uppyDashboard.on("complete", (result) => {
        if (result.failed.length === 0) {
          console.log("Upload successful");
        } else {
          console.warn("Upload failed");
        }
        console.log("successful files:", result.successful);
        console.log("failed files:", result.failed);
      });
})
$: viewUppy = false ;
const handleViewUppy = () =>{ 
  viewUppy = !viewUppy
  console.log(viewUppy)
  }
</script>
<div class="w-full flex items-center justify-center">
  <button on:click={handleViewUppy} class="bg-green-400 p-5 rounded m-10">Upload Files</button>
</div>

<div class={`${ viewUppy ? " flex ":" hidden "} z-30 backdrop-blur-lg min-h-[100vh] flex-col items-center justify-center fixed top-0 left-0 w-full h-full overflow-hidden `}>
  <button on:click={handleViewUppy} class="bg-pink-400 p-3 font-bold rounded m-5">Close</button>
  <div id="app"  />

</div>