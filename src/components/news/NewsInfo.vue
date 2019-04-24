<template>
  <div class="newsinfo-container">
    <!-- 大标题 -->
    <h3 class="title">{{ newsinfo.title }}</h3>
    <!-- 子标题 -->
    <p class="subtitle">
      <span>发表时间：{{ newsinfo.aid }}</span>
      <span>点击：{{ newsinfo.catid }}次</span>
    </p>

    <hr>
    <!-- 内容 -->
    <div class="content" v-html="newsinfo.content"></div>
    <!-- 评论区子组件 -->
    <comment-box :id="this.id"></comment-box>
  </div>
</template>
<script>
import { Toast } from "mint-ui";
import comment from "../subcomponents/comment.vue";
export default {
  data() {
    return {
      id: this.$route.params.id,
      newsinfo: {}
    };
  },
  created() {
    this.getNewsInfo();
  },
  methods: {
    getNewsInfo() {
      this.$http
        .get("appapi.php?a=getPortalArticle&aid=" + this.id)
        .then(result => {
          if (result.body.result) {
            console.log(result.body);
            this.newsinfo = result.body.result[0];
          } else {
            Toast("获取新闻失败");
          }
        });
    }
  },
  components: {
    "comment-box": comment
  }
};
</script>
<style lang="scss" >
.newsinfo-container {
  padding: 0px 4px;
  .title {
    font-style: 16px;
    margin: 15px 0px;
    text-align: center;
    color: red;
  }

  .subtitle {
    font-size: 13px;
    color: #226aff;
    display: flex;
    justify-content: space-between;
  }
  .content {
    img {
      width: 100%;
    }
  }
}
</style>


