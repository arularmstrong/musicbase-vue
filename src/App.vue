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
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.three-inline-buttons .button {
    margin-left: 15px;
    margin-right: 15px;
}

.three-inline-buttons {
     display: table;
     margin: 0 auto;
}



.list{
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 20%;
  text-align: left;
}

</style>
