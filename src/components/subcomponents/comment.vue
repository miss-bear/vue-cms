<template>
  <div class="cmt-container">
    <h3>发表评论</h3>
    <hr>
    <textarea placeholder="请输入BB的内容（最多吐槽120字）" maxlength="120"></textarea>
    <mt-button type="primary" size="large">发表评论</mt-button>
    <div class="cmt-list">
      <div class="cmt-item" v-for="(item,i) in comments" :key="item.aid">
        <div
          class="cmt-title"
        >第{{ i+1 }}楼&nbsp;&nbsp;用户:{{ item.username }}&nbsp;&nbsp;发表时间:{{ item.dateline | dateFormat('YYYY-MM-DD HH:mm:ss') === 'Invalid date' ? '2012-12-12 12:12:12' : '2019-04-23 12:12:12'}}</div>
        <div class="cmt-body">{{ item.title }}</div>
      </div>
    </div>
    <mt-button type="danger" size="large" plain @click="getMore">加载更多</mt-button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      comments: []
    };
  },
  created() {
    console.log("*************************");
    this.getComments();
  },
  methods: {
    getComments() {
      this.$http
        .get("appapi.php?a=getPortalList&catid=20&page=1")
        .then(result => {
          console.log("=======================================");
          console.log(result.body);
          if (result.body.result) {
            console.log("%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%");
            this.comments = this.comments.concat(result.body.result);
          } else {
            Toast("获取评论失败！");
          }
        });
    },
    getMore(){
        this.getComments();
    }
  },
  props: ["id"]
};
</script>
<style lang="scss" scoped>
.cmt-container {
  h3 {
    font-size: 18px;
  }
  textarea {
    font-size: 14px;
    height: 85px;
    margin: 0;
  }
  .cmt-list {
    margin: 5px 0;
    .cmt-item {
      font-size: 12px;
      .cmt-title {
        line-height: 30px;
        background-color: #ccc;
      }
      .cmt-body {
        line-height: 35px;
        text-indent: 2em;
      }
    }
  }
}
</style>


