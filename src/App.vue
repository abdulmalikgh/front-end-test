<template>
  <div id="app">
    <Main />
  </div>
</template>

<script>
import Main from './components/Main'
export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style>
html, body{
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Open Sans', Arial, Helvetica, sans-serif;
  position: relative;
  color: #202020;
  font-size: 14px;
  min-width: 1024px;
}
a {
  color: #008ad6;
  text-decoration: none;
}
a.disabled {
  opacity: 0.5;
  filter: alpha(opacity=50);
  cursor: not-allowed;
  pointer-events: none;
}
a:focus,
.btn:focus,
a:active,
.btn:active,
a:active:focus,
.btn:active:focus,
a.active:focus,
.btn.active:focus {
  outline: 0;
}
</style>
