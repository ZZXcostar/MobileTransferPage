<template>
  <div id="app">
    <p style='font-size:16px;text-align:center;' v-show="isPresentation == 'no'?true:false">跳转中...</p>
    <p style='font-size:16px;text-align:center;' v-show="isPresentation == 'is'?true:false">请稍等...</p>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data (){
    return{
      isPresentation:''
    }
  },
  created() {
     let isTrues = this.$route.query.json;
     //alert(isTrues.presentation)
      if(isTrues.presentation != null || isTrues.presentation !=undefined){
        this.isPresentation = 'is';
      }else{
      this.isPresentation = 'no';
     }
  },
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
</style>
