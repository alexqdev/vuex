<template>
  <footer><p>&copy; 2021</p></footer>
</template>
<script>
  export default {
    name:'Footer',
  }
</script>
<style lang="less" scoped>
@import "../styles/_variables.less";

footer{
  position: fixed;
  bottom: 0;
  left: 0;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-top: 1px solid @primary-color;
  background: @primary-color-dark;
  width: 100%;
}
@media screen and (min-width: 768px){
  footer{
    height: 40px;
  }
}
</style>