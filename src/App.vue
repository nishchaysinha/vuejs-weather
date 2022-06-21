<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search for a Place..."/>
      </div>
    </main>
  </div>
</template>

<script>
  export default {
    name: "app",
    data(){
      api_key: '323859ab1dd9648172b8ab428b2d89f5'
    }
  } 
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'monserrat', sans-serif;

}
#app{
  background-image: url('./assets/cold.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main{
  min-height: 100vh;
  padding: 75px;
}

</style>