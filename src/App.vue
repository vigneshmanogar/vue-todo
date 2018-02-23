<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Merriweather:400,400i,700');

* {
  box-sizing: border-box;
}

body {
  padding: 0px;
  margin: 0px;
}

::-webkit-input-placeholder {
  font-family: 'Merriweather', serif;
}

#app {
  font-family: 'Merriweather', serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;

  display: inline-block;
  width: 100%;
  min-height: 100vh;
  color: #333;
}

button {
  font-family: 'Merriweather', serif;
  display: inline-block;
  vertical-align: top;
  background: transparent;
  border: 0px;
  height: 34px;
  width: 60px;
  margin: 0px 5px;
  text-align: center;
  color: #999;
  text-transform: capitalize;
}

button:hover {
  cursor: pointer;
}
</style>
