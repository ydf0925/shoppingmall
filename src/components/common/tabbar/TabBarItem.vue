<template>
    <div class="tab-bar-item" @click="btnClick">
        <div v-if="!isActive"><slot name="item-icon"></slot></div>
        <div v-else><slot name="item-icon-active"></slot></div>
        <div :style="isActiveStyle"><slot name="item-text"></slot></div>
    </div>
   
</template>

<script>
   export default {
       name:'TabBarItem',
       props:{
         path:String,
         styleColor:{
           type: String,
           default: 'red'
         }
       },
      computed:{
        isActive() {
          return this.$route.path.indexOf(this.path) !== -1
        },
        isActiveStyle() {
          return this.isActive ? {color:this.styleColor} : {}
        }
      },
       methods:{
         btnClick() {
           this.$router.push(this.path)
         }
       }
   }
</script>

<style scoped>
.tab-bar-item {
  flex: 1;
  text-align: center;
  font-size: 14px;
  height: 49px;
}
.tab-bar-item img {
  width: 24px;
  height: 24px;
  margin-top: 3px;
  vertical-align: middle;
}
/* .active {
  color: orange;
} */
</style>