<template>
  <div class="main">
    <div class="page-container">
      <!-- contains only side navigation -->
      <div id="sideNavigation">
          <ul>
            <li>
              <p>
                Backgrounds
              </p>
            </li>
            <ul>
              <li>
                <p>
                  Frames
                </p>
              </li>
            </ul>
          </ul>
      </div>

      <!-- contains the background, frame and image -->
      <div id="wallpaper">

      </div>

    <div class="bottomNavigation">
      <button class="btn">Upload Image(s)</button>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'main-images-component',
  props: {
    msg: String
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
    margin:0px;
    padding:0px;
    li{
      display: flex;
      justify-content: center;
      align-items: center;
      color:#fff;
      background-color: #008ad6;
      width:100px;
      height: 50px;
      cursor: pointer;
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
/* wall paper */
#wallpaper{
  background: url('../assets/wallpapers/wall1.jpg');
  min-width: 730px;
  text-align: center;
  position: absolute;
  top: 0;
  left: 100px;
  bottom: 90px;
  right: 80px;
  overflow: hidden;
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
}
.bottomNavigation .btn{
  color:#fff;
  background-color: #008ad6;
  outline: none;
  border:none;
  width: 300px;
  max-width: 50%;
  height: 30px;
  cursor: pointer;
}
</style>
