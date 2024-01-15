<script>
    import OpenPopUp from "./OpenPopUp.svelte";
    import {dropMenuData} from "./../../constants/DropMenuData"
	import Icon from '@iconify/svelte';
    import "../uppy-custom.css"

    $: viewUploadOptions = false ;
    const handleViewUploadOptions = ()=>{
        viewUploadOptions = !viewUploadOptions
    }
    $: openUppyPopUp = undefined ;
    const handleOpenUppyPopup = (reqOpenSection)=>{
        if(openUppyPopUp != reqOpenSection){
            viewUploadOptions = false
            openUppyPopUp = reqOpenSection ;
        }else{
            openUppyPopUp = undefined ;
            viewUploadOptions = false
        }
    }
    
</script>
<div class="text-white  backdrop-blur-sm">
    <div class="w-full flex flex-col items-center justify-center p-5 bg-white/20">
        <div id="UppyMain" class=" relative flex items-center justify-center w-1/4 gap-1 p-2">
            <button id="uploadFile" class=" p-3 bg-cyan-400 hover:bg-cyan-500 text-slate-900 uppercase text-sm rounded w-full font-bold">Upload File</button>
            <button on:click={handleViewUploadOptions} class="bg-cyan-400 hover:bg-cyan-500 text-black text-xl p-3 rounded">
                <Icon icon="pepicons-pencil:dots-x" />
            </button>
            <div class={`${viewUploadOptions ? " block " : "hidden"} absolute top-[100%] right-0 flex flex-col bg-slate-900  z-[2000] items-start p-3 gap-3 mx-2 rounded`}>
                {#each dropMenuData as {name,icon,value}}
                     <button on:click={()=>{handleOpenUppyPopup(value)}} id={value} class="flex items-center gap-3 pr-5 hover:bg-slate-800  transition-all ease-in w-full p-2 rounded capitalize">
                        <div class="text-2xl">
                            <Icon icon={icon}/>
                        </div>
                        <h4>{name}</h4>
                    </button>
                {/each}
            </div>
        </div>
        <div class="w-1/4">
            <OpenPopUp openUppyPopUp={openUppyPopUp}/>
        </div>
    </div>
</div>