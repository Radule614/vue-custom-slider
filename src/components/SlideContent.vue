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
  width: 300px;
  height: 300px;
  font-size: 17px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>