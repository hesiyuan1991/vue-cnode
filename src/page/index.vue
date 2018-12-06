<template>
  <div>
    <myHeader></myHeader>
    <el-main class="article_list content">
      <el-tabs v-model="editableTabsValue" @tab-click="tabClick" class="tabNav">
        <el-tab-pane
          v-for="(item, index) in editableTabs"
          :key="item.name"
          :label="item.title"
          :name="item.name"
        >
          <ul class="list">
            <li v-for="i in list">
              <a href="#" class="countImg">
                <img :src="i.author.avatar_url" :title="i.author.loginname" />
              </a>

              <i class="total">{{i.reply_count}}/{{i.visit_count}}</i>


              <template v-if="item.name ==='all'" class="nameTag">
                <span class="nameTag green" v-if="i.good === true">精华</span>
                <span class="nameTag green" v-else-if="i.top === true">置顶</span>
                <span class="nameTag" v-else-if="i.tab === 'ask'">问答</span>
                <span class="nameTag" v-else-if="i.tab === 'job'">招聘</span>
                <span class="nameTag" v-else-if="i.tab === 'share'">分享</span>
                <span class="nameTag" v-else-if="i.tab === 'dev'">客户端测试</span>
              </template>
              <template v-else-if="item.name ==='good'" >
                <span class="nameTag green">精华</span>
              </template>
              <template v-else >
                <template  v-if="i.good === true"><span class="nameTag green">精华</span></template >
              </template>

              <router-link :to="'/content/' + i.id" class="listContent">
                {{ i.title }}
              </router-link>


              <a href="#" class="lastCountImg">
                <img :src="i.author.avatar_url" :title="i.author.loginname">
                <time class="time" v-text="$utils.goodTime(i.last_reply_at)"></time>
              </a>
            </li>
          </ul>
        </el-tab-pane>
      </el-tabs>

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
        list: [],
        editableTabsValue: 'all',
        editableTabs: [{
          title: '全部',
          name: 'all'
        }, {
          title: '精华',
          name: 'good'
        }, {
          title: '分享',
          name: 'share'
        }, {
          title: '问答',
          name: 'ask'
        }, {
          title: '招聘',
          name: 'job'
        }, {
          title: '客户端测试',
          name: 'dev'
        }]
      }
    },
    created () {
      this.getData()
    },
    methods: {
      getData () {
        this.$api.get('topics', null, r => {
          this.list = r.data
        })
      },
      tabClick (tab) {
        let name = tab.name,
            $list = this.list = [];

        if(name === 'all'){
          this.$api.get('topics', null, r => {
            this.list = r.data
          })
        }else if(name === 'good'){

          this.$api.get('topics', {
            tab : 'good',
            limit:40
          }, r => {
            this.list = r.data
          })

        }else{
          this.$api.get('topics', {
            tab : name,
            limit:40
          }, r => {
            let data = r.data;
            for (let i=0 ; i<data.length ; i++){
            if(data[i].tab === name){
              $list.push(data[i])
            }
            }
          });
        }
      }
    }
  }
</script>
