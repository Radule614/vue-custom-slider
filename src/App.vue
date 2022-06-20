<script>
import CustomSlider from './components/CustomSlider.vue'

export default {
  name: 'App',
  data(){
    return {
      dataArray: [
        {
          content: 'A'
        },
        {
          content: 'B'
        },
        {
          content: 'C'
        },
        {
          content: 'D'
        },
        {
          content: 'E'
        },
        {
          content: 'F'
        },
        {
          content: 'G'
        },
        {
          content: 'H'
        },
        {
          content: 'I'
        },
        {
          content: 'J'
        },
        {
          content: 'K'
        }
      ]
    }
  },
  components: {
    CustomSlider
  }
}
</script>

<template>
  <custom-slider :item-array="dataArray"/>
</template>

<style>
body{
  background-color: #f9f9f9;
  margin:0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 150px;
}
</style>
