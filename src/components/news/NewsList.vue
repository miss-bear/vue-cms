<template>
  <div>
    <ul class="mui-table-view">
      <li class="mui-table-view-cell mui-media" v-for="item in newsList" :key="item.aid">
        <router-link :to="'/home/newsinfo/' + item.aid">
          <img
            class="mui-media-object mui-pull-left"
            src="http://img3.imgtn.bdimg.com/it/u=1500868681,3841300386&fm=26&gp=0.jpg"
          >
          <div class="mui-media-body">
            <h1> {{ item.title }}</h1>
            <p class="mui-ellipsis">
              <span>发表时间：{{ item.dateline }}</span>
              <span>点击次数：{{ item.aid }}次</span>
            </p>
          </div>
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import { Toast } from "mint-ui"
export default {
    data(){
        return{
            newsList: []
        }
    },
    created(){
      this.getNewsList()
    },
    methods:{
        getNewsList(){
            // this.$http.get('http://www.phonegap100.com/appapi.php?a=getPortalList&catid=20&page=2').then( result => {
            this.$http.get('appapi.php?a=getPortalList&catid=20&page=1').then( result => {
              if(result.body.result){
                this.newsList = result.body.result
                console.log(result.body)
              }else{
                Toast('获取新闻列表失败')
              }
            })
        }
    }
};
</script>

<style lang="scss" scoped>
.mui-table-view {
  li {
    h1 {
        font-size: 14px;
    }
    .mui-ellipsis {
        font-size: 12px;
        color: #226aff;
        display: flex;
        justify-content: space-between;
    }
  }
}
</style>

