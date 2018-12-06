<template>
  <div>
    <myHeader></myHeader>
    <el-main class="content">
      <div class="detailContent">
        <div class="topic_header">
          <h2 v-text="dat.title"></h2>
          <div class="changes">
            <span>发布于：{{$utils.goodTime(dat.create_at)}}</span>
            <span>作者：<router-link class="goDetail" :to="'/'" >{{dat.author.loginname}}</router-link></span>
            <span>{{dat.visit_count}} 次浏览</span>
            <span>来自 {{dat.tab}}</span>
          </div>
        </div>
        <div class="topic">
          <article v-html="dat.content"></article>
        </div>
      </div>
      <div class="replyContent">
        <h3 class="replyTitle">{{dat.reply_count}} 回复</h3>
        <ul>
          <li v-for="(i , index) in dat.replies">
            <a href="#" class="user_avatar">
              <img :src="i.author.avatar_url" :title="i.author.loginname" />
            </a>
            <div class="user_info">
              <a class="reply_author" href="#">{{i.author.loginname}}</a>
              <a class="reply_time" :href="'#' + i.id">{{index+1}}楼•{{$utils.goodTime(i.create_at)}}</a>
            </div>
            <article v-html="i.content" class="reply_content from-ugrg"></article>
          </li>
        </ul>
      </div>
    </el-main>
    <myFooter></myFooter>
  </div>
</template>
<script>
  import myHeader from '../components/header.vue'
  import myFooter from '../components/footer.vue'
  export default {
    components: { myHeader, myFooter },
    data () {
      return {
        id: this.$route.params.id,
        dat: {
          author: {
          }
        }
      };
    },
    created () {
      this.getData()
    },
    methods: {
      getData () {
        this.$api.get('topic/' + this.id, null, r => {
          this.dat = r.data;
          console.log( this.dat);
        })

      }
    }
  }
</script>
