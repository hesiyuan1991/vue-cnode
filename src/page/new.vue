<template>
  <div>
    <myHeader></myHeader>
    <el-main class="content">
      <el-form ref="form" :model="form" label-width="80px">
        <el-form-item label="主题名称">
          <el-input v-model="form.title"></el-input>
        </el-form-item>
        <el-form-item label="主题内容">
          <el-input type="textarea" v-model="form.content"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm">提交</el-button>
        </el-form-item>
      </el-form>
    </el-main>
    <myFooter></myFooter>
  </div>
</template>
<script>
  import myHeader from '../components/header.vue'
  import myFooter from '../components/footer.vue'
  export default {
    components: { myHeader, myFooter },
    data() {
      return {
        form: {
          title: '',
          content: ''
        }
      }
    },
    methods: {
      submitForm() {
        let config = {
          accesstoken : 'c04add5c-1184-455c-b2c3-5db956129301',
          title  : this.form.title,
          content   : this.form.content ,
          tab : 'dev'
        }

        this.$api.post('topics', config)
      }
    }
  }
</script>
