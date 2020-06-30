<template>
   <div class="recommend">
       <div v-for="(item,index) in this.recommends" :key=index class="recommend-item">
         <a :href="item.link">
            <img :src="item.image">
         </a>
         <div>{{item.title}}</div>
       </div>
   </div>
</template>

<script>
   export default {
       name:'RecommendView',
       props:{
         recommends: {
           type: Array,
           default() {
             return []
           }
         }
       }
   }
</script>

<style scoped>
.recommend {
  display: flex;
  width: 100%;
  text-align: center;
  font-size: 14px;
  padding: 10px 0 20px;
  border-bottom: 8px sloid #eee;
}

.recommend-item {
  flex: 1;
}
.recommend-item img {
  width: 70px;
  height: 70px;
  margin-bottom: 10px;
}
</style>