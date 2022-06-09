<template>
  <div class="content">
    <h4>
      {{ title }}
    </h4>
    <div class="images-container">
      <ul class="image-list">
        <li class="image-list-item" v-for="(image, key) in images" 
          :key="key" @click="setActive(image)" 
          :class="[image.active  ? 'active' :'']">
          <img :src="image.image" alt="">
        </li>
      </ul>
    </div>
    <div class="fileUploadContainer">
        <input @change="handleFileChange" type="file" itemid name="" 
          accept="image/png, image/jpg, image/jpeg" ref="file" id="fileUpload">
        <button id="uploadBtn" @click="uploadFile" class="btn">
          {{ btnText }}
        </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title:{
      type: String,
      required: true
    },
    images:{
      type: Array,
      required: true
    },
    btnText: {
      type: String,
      required: true
    }
  },
  data(){
    return {

    }
  },
  methods:{
    setActive(image){
      this.$emit('setActive', image)
    },
    uploadFile() {
      this.$refs.file.click()
    },
    handleFileChange(e) {
      this.$emit('fileUpload', e.target.files[0])
      this.type = 'frames'
    }
  }
}
</script>

<style lang="scss" scoped>
.content{
  width:100%;
  h2{
    font-size: 13px;
    font-weight: bold;
  }
  // IMAGE CARDS CONTAINER
  .images-container{
    .image-list{
      width:100%;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      .image-list-item{
        width: 100px;
        height: 100px;
        margin-bottom: 20px;
        background-color: #eeeeee;
        -webkit-box-shadow: 1px 1px 0 #cad0d2, -1px -1px 0 #cad0d2, 1px -1px 0 #cad0d2, -1px 1px 0 #cad0d2;
        -moz-box-shadow: 1px 1px 0 #cad0d2, -1px -1px 0 #cad0d2, 1px -1px 0 #cad0d2, -1px 1px 0 #cad0d2;
        box-shadow: 1px 1px 0 #cad0d2, -1px -1px 0 #cad0d2, 1px -1px 0 #cad0d2, -1px 1px 0 #cad0d2;
        img{
          height: 100%;
          width: 100%;
        }
        &:hover{
          -webkit-box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
          -moz-box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
          box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
        }
      }
    }
  }

  //SET BORDER TO ACTIVE IMAGE OR SELECTED IMAGE
  .active{
    -webkit-box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
    -moz-box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
    box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
  }
  // FILE UPLOAD CONTENT
  .fileUploadContainer{
    margin-top: 2em;
    #uploadBtn{
      width: 100%;
    }
    #fileUpload{
      display: none;
    }
  }
}
</style>