<template>
  <div>
      <img v-bind:src="imgSrc" width="200px"/>
    <p><a :href="weburl" target="_blank">周川</a> </p>
    <div></div>
    <zhouchuan></zhouchuan>
  </div>
</template>

<script>
  // Vue.component('zhouchuan',{
  //   template:`  `
  // });
  export default {
    name: 'hello',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App',
        imgSrc:'https://www.csdn.net/app/img/iPhone.png',
        weburl:'https://www.colabug.com/2203840.html'
      }
    },
    mounted(){

    },
    methods: {

    }
  }
</script>

<style scoped>

</style>
