<template>
   <div id="home">
       <NavBar class="home-nav"><div slot="middle">购物街</div></NavBar>
       <HomeSwiper :banners="banners"/>
       <RecommendView :recommends="recommends" class="recommend-view"/>
       <FeatureView/>
       <TabControl :titles="['流行','新款','精选']" class="tab-control"/>
       <GoodsList :goods="goods['pop'].list"/>
   </div>
</template>

<script>
import HomeSwiper from './childcomps/HomeSwiper'
import RecommendView from './childcomps/RecommendView'
import FeatureView from './childcomps/FeatureView'

import NavBar from 'components/common/navbar/NavBar'
import TabControl from 'components/content/tabControl/TabControl'
import GoodsList from 'components/content/goods/GoodsList'

import {getHomeMultidata,getHomeGoods} from 'network/home'

   export default {
       name:'Home',
       components: {
           HomeSwiper,
           RecommendView,
           FeatureView,
           NavBar,
           TabControl,
           GoodsList
       },
       data() {
           return {
               banners: [],
               recommends: [],
               goods: {
                   'pop': {page: 0,list: []},
                   'new': {page: 0,list: []},
                   'sell': {page: 0,list: []}
               }
           }
       },
       created() {
           this.getHomeMultidata()
           this.getHomeGoods('pop')
           this.getHomeGoods('new')
           this.getHomeGoods('sell')  
       },
       methods: {
            getHomeMultidata() {
                getHomeMultidata().then(res => {
                    console.log(res);
                    this.banners = res.data.banner.list
                    this.recommends = res.data.recommend.list
                })
            },
            getHomeGoods(type) {
                const page = this.goods[type].page + 1
                getHomeGoods(type,page).then(res => {
                    this.goods[type].list.push(...res.data.list)
                    this.goods[type].page += 1
           })
            }
       }
   }
</script>

<style scoped>
#home {
    padding-top: 44px;
}

.home-nav {
    background-color: var(--color-tint);
    color: #fff;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 9;
}

.tab-control {
    position: sticky;
    top: 44px;
    z-index: 9;
}
</style>