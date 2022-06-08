<template>
  <div class="content">
    <h4>
      {{ title }}
    </h4>
    <div class="images-container">
      <ul class="image-list">
        <li class="image-list-item" v-for="(image, key) in images" :key="key" @click="setActive(image)" :class="[image.active  ? 'active' :'']">
          <img :src="image.image" alt="">
        </li>
      </ul>
    </div>
    <div class="fileUploadContainer">
        <!-- <input type="file" name="" accept="image/png, image/jpg, image/jpeg" id="fileUpload">
        <button>
          {{ btnText }}
        </button> -->
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
    }
  }
}
</script>

<style lang="scss" scoped>
.content{
  width:100%;
  h2{
    font-size: 13px;
  }
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

  //
  .active{
    -webkit-box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
    -moz-box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
    box-shadow: 2px 2px 0 #29bdb3, -2px -2px 0 #29bdb3, 2px -2px 0 #29bdb3, -2px 2px 0 #29bdb3!important;
  }
}
</style>