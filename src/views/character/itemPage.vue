<template>
    <div class="group-flex-phone" style="gap: 50px">
      <div class="group-flex-col f-1" style="gap: 20px">
        <span class="title">Roblox Item Downloader!</span>
        <span class="desc">This page used for downloading the roblox catalog items (only 3D items), and you can use this as a props for your gfx. You may ask where is the item id, here the example roblox item url: 'https://www.roblox.com/catalog/1000'
          
          the '1000' number is the id, you can copy the id and use it in here for downloading the items.
        </span>
      </div>
      <div class="group-flex-col f-1">
        <div class="group-flex-row">
          <input type="number" id="inputType" placeholder="Type the roblox item id in here! (Only for 3D items)" v-model="item_id">
          <button id="downloadBtn" aria-label="inputType" @click.prevent="downloadItem()">
            <i class="mdi mdi-download"></i>
          </button>
        </div>
      </div>
    </div>
</template>

<script>
  import { ax, swalToast, downloadFile } from '@/lib/webLib.js';
  
  export default{
    data() {
      return{
        item_id: ''
      }
    },
    methods: {
      async downloadItem() {
        try {
          await swalToast("warning", "Please wait!");
          await downloadFile(`/api/v1/item/download3d?i=${this.item_id}`, `item_${this.item_id}.zip`)
        } catch(err) {
          //swalToast("error", err['message'])
          console.error(err)
          await swalToast("error", "Something went wrong! (item didnt exist or maybe there's an error!")
        }
      }
    }
  }
</script>