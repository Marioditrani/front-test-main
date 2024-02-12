<script >
  
  import AppNav from './components/AppNav.vue'


  export default {
  components:{  AppNav }
  }
</script>

<template>

  <div class="container">
    <AppNav />
    <router-view class="page"></router-view>
  </div>
 

  
</template>

<style lang="scss">
@use './assets/styles/general.scss' as *;
.page::-webkit-scrollbar{
  width: 10px;
}
.page::-webkit-scrollbar-thumb {
  border-radius: 20px;
  background: $c-header;
}
.page::-webkit-scrollbar-thumb:hover {
  border-radius: 20px;
  background-color: $c-nav-link;
  border: 2px solid $c-header;
    
}
body{
  background-color: $c-bg;
}

.container{
  display: flex;
  flex-direction: column;
  height: 100vh;
  padding: 0;
  overflow: hidden;
}
.page{
    // position: fixed;
    // top: 0;
    // right: 0;
    width: 100vw;
    padding: 0 2rem ;
    overflow: auto;
    height: 100% ;
    margin-top: 230px;
    padding-bottom: 50vh;
}


@media (max-width:$bp1) {
  .page{
    width: 100%;
  }
  
}


body::-webkit-scrollbar{
  width: 10px;
}
body::-webkit-scrollbar-thumb {
  border-radius: 20px;
  background: $c-header;
}
body::-webkit-scrollbar-thumb:hover {
  border-radius: 20px;
  background-color: $c-nav-link;
  border: 2px solid $c-header;
    
}

</style>
