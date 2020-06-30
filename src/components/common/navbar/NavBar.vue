<template>
   <div class="nav-bar">
       <div class="left"><slot name="left"></slot></div>
       <div class="middle"><slot name="middle"></slot></div>
       <div class="right"><slot name="right"></slot></div>
   </div>
</template>

<script>
   export default {
       name:'NavBar'
   }
</script>

<style scoped>
.nav-bar {
  display: flex;
  height: 44px;
  line-height: 44px;
  text-align: center;
  box-shadow: 0px 1px 1px rgba(100, 100, 100, .3);
}

.left,.right {
  width: 100px;
}

.middle {
  flex: 1;
}
</style>