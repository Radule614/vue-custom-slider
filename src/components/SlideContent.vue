<script>
export default{
  props: {
    item:{
      content: String
    }
  }
}
</script>

<template>
  <div class="slide">
    {{item.content}}
  </div>
</template>

<style scoped>
.slide{
  padding:170px;
  font-size: 17px;
}
</style>