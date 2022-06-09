<template>
  <div class="main">
    <div class="page-container">
      <!-- contains only side navigation -->
      <div id="sideNavigation">
          <ul>
            <li :class="[type == 'backgrounds' ? 'activeSidePane' :'']" @click="togglePane('backgrounds')">
              <p>
                Backgrounds
              </p>
            </li>
            <ul>
              <li v-if="uploadedImages.length" :class="[type == 'frames' ? 'activeSidePane' :'']" @click="togglePane('frames')">
                <p>
                  Frames
                </p>
              </li>
            </ul>
          </ul>
      </div>
      
      <!-- side pain -->
      <div id="sidePane" v-if="hidePane">
        <div class="backgrounds">
          <SelectImagesComponent 
            @setActive="setActive" 
            v-if="type == 'backgrounds'" 
            :title="'Select Background'" 
            :images="backgrounds"
            :btnText="'Upload Background Image'"
            @fileUpload="fileUpload" />
          <SelectImagesComponent 
            @setActive="setActive" 
            v-if="type == 'frames'" 
            :title="'Select Frame'" 
            :images="frames"
            :btnText="'Upload Frame'"
            @fileUpload="fileUpload" />
        </div>
      </div>
      <!-- contains the background, frame and image -->
      <div id="wallpaper">
        <div class="wallPaperInner" id="wallpaperInner">
          
        </div>
      </div>

    <div class="bottomNavigation">
      <input 
        type="file" 
        accept="image/jpeg, image/png, image/jpg" 
        ref="file" 
        multiple="multiple"
        @change="handleUploadImages"
        id="uploadImages">
      <button @click="uploadFile" class="btn">Upload Image(s)</button>
    </div>
    </div>
  </div>
</template>

<script>
import backgrounds from '../helpers/backgrounds'
import frames from '../helpers/frames'
import SelectImagesComponent from '../components/SelectImagesComponent.vue'
export default {
  name: 'main-images-component',
  components: {
    SelectImagesComponent
  },
  data() {
    return {
      hidePane: false,
      type: '',
      uploadFrame: false,
      backgrounds: backgrounds,
      frames: frames,
      uploadedImages: [],
      width: '400px',
      height: '400px',
      frameInnerHeight: '350px',
      frameInnerWidth: '350px',
      frameImage:null,
    }
  },
  methods:{
     setFrameBackground() {
        //set frame image
        let image = this.frameImage
        let wallpaperInnerContainer = document.getElementById('wallpaperInner')
        wallpaperInnerContainer.textContent = ''
        for(let i = 0; i < this.uploadedImages.length; i++) {
          //create frame and style it
          let frame = document.createElement('div');
          frame.style.width = this.width
          frame.style.height = this.width
          frame.style.backgroundRepeat = 'no-repeat'
          frame.style.backgroundSize = '100% 100%'
          frame.style.boxShadow = '4px 0 4px -4px rgba(0, 0, 0, 0.45)'
          frame.style.display = 'flex'
          frame.style.justifyContent = 'center'
          frame.style.alignItems = 'center'
          frame.style.margin = '15px'
          
          //check whether the user uploaded his own frame or use provided frames
          if(image && image.image) {
            //if user select from provided frames set it as frame background
            frame.style.backgroundImage = `url(${image.image})`
          } else {
            // if user uploaded own frame , set create url for the image
            const reader = new FileReader();
            reader.addEventListener("load", function () {
            frame.style.backgroundImage = `url(${reader.result})`
            }, false);
            if(image) reader.readAsDataURL(image);
          }
          //create container to hold frame image
          let frameInner = document.createElement('div');
          frameInner.style.width = this.frameInnerWidth
          frameInner.style.height = this.frameInnerHeight
          //create new Image
          const reader = new FileReader();
          let frameImage = document.createElement('img');
          reader.addEventListener("load", function () {
            //set image width and height as it's parent width and height
            frameImage.style.height = '100%'
            frameImage.style.width = '100%'
            frameImage.src = reader.result;
            frameImage.padding = '30px'
            //Insert created image into the inner frame component created
            frameInner.appendChild(frameImage)
          }, false);
          if(this.uploadedImages[i]) reader.readAsDataURL(this.uploadedImages[i]);
          frame.appendChild(frameInner)
          //add frame to the dom
          wallpaperInnerContainer.appendChild(frame)
        }
       
     },
    uploadFile() {
      this.$refs.file.click()
    },
    handleUploadImages(e) {
      this.uploadedImages =  e.target.files
      this.type = 'frames'
      this.hidePane = true
      //if user has already selected a frame should it instead and add images
      if(this.frameImage) {
        this.setFrameBackground()
      }
    },
    fileUpload(image) {
      //Get background image 
      if(this.type === 'backgrounds') {
        const background = document.getElementById('wallpaper')
        const reader = new FileReader();
        reader.addEventListener("load", function () {
          background.style.backgroundImage = `url(${ reader.result })`;
        }, false);
        if(image) reader.readAsDataURL(image);
      } else {
        this.frameImage = image
        this.setFrameBackground()
      }
    },
    changeBackgroundImage(image){
      //get background image 
      const background = document.getElementById('wallpaper')
      //set background image to the selected image
      background.style.backgroundImage = `url(${image})`
    },
    setActive(image) {
      //get active or selected image from user 
      //set the select image as active and then reset other images active to false
      if(this.type === 'backgrounds') {
          this.backgrounds.forEach(background => {
          if(background.id == image.id) {
            background.active = !background.active
          } else {
            background.active = false
          }
        })
        this.changeBackgroundImage(image.image)
      } else {
        this.frames.forEach(frame => {
          if(frame.id == image.id) {
            frame.active = !frame.active
          } else {
            frame.active = false
          }
        })
        this.frameImage = image
        this.setFrameBackground()
      }
    },
    togglePane(type) {
      //show and hide frames or background images content
      if(this.type == type) {
        this.hidePane = false
        this.type = ''
      } else {
        this.hidePane = true
        this.type = type
      }
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
/* main page styles */
.main{
  width:100%;
  height: 100vh;
  margin: none;
  padding: none;
  position: relative;
  background: #000;
  overflow: hidden;
}

/* side navigation */
#sideNavigation{
  width: 100px;
  height: calc(100vh - 90px);
  display:flex;
  justify-content: center;
  padding:0px;
  ul {
    li{
      display: flex;
      justify-content: center;
      align-items: center;
      color:#fff;
      background-color: #008ad6;
      width:100px;
      height: 50px;
      &:hover{
        color:#008ad6;
        background-color: #fff 
      }
      &:not(:last-child){
        border-bottom: 1px solid #fff;
      }
    }
  }
}
.activeSidePane{
  color:#008ad6!important;
  background-color: #fff!important
}
/* SIDE PANE */
#sidePane{
  width:250px;
  height: 100vh;
  display: flex;
  position: absolute;
  left:100px;
  bottom:0;
  top:0;
  background:#fff;
  z-index:100;
  .backgrounds{
    padding: 15px;
  }
}
/* wall paper */
#wallpaper{
  background: url('../assets/backgrounds/wall1.jpg');
  min-width: 730px;
  text-align: center;
  position: absolute;
  top: 0;
  left: 100px;
  bottom: 90px;
  right: 0px;
  overflow: hidden;
  background-repeat: no-repeat;
  background-size: 100% 100%;
  -webkit-user-select: none;
  /* Chrome all / Safari all */
  -moz-user-select: none;
  /* Firefox all */
  -ms-user-select: none;
  /* IE 10+ */
  /* No support for these yet, use at own risk */
  -o-user-select: none;
  user-select: none;
  -webkit-box-shadow: 4px 0 4px -4px rgba(0, 0, 0, 0.45);
  -moz-box-shadow: 4px 0 4px -4px rgba(0, 0, 0, 0.45);
  box-shadow: 4px 0 4px -4px rgba(0, 0, 0, 0.45);
  .wallPaperInner{
   width: 100%;
   height: 100%;
   display: flex;
   justify-content: center;
   align-items:center;
   flex-wrap: wrap;
  }
}
.frameImage{
  width: 400px;
  height: 400px;
  -o-user-select: none;
  user-select: none;
  -webkit-box-shadow: 4px 0 4px -4px rgba(0, 0, 0, 0.45);
  -moz-box-shadow: 4px 0 4px -4px rgba(0, 0, 0, 0.45);
  box-shadow: 4px 0 4px -4px rgba(0, 0, 0, 0.45);
  background-repeat: no-repeat;
  background-size: 100% 100%;
  z-index: 100;
  padding: 30px;
}
/* Bottom Navigation */
.bottomNavigation{
  width: 100%;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 20px;
  #uploadImages{
    display: none;
  }
  .btn{
    width: 250px;
  }
}
</style>
