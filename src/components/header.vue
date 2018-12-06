<template>
  <el-header class="header">
    <el-row class="logo">
      <el-col :span="3" :offset="1">
        <a href="https://cnodejs.org" target="_blank" class="logoImg">
          <img src="static/image/cnodejs_light.svg" alt="logo" >
        </a>
      </el-col>
      <el-col :span="6">
        <input type="text">
      </el-col>
      <el-col :span="8" :offset="6">
        <el-row class="link">
          <el-col :span="4">
            <router-link class="goDetail" :to="'/'" >首页</router-link>
          </el-col>
          <el-col :span="4"><a href="#">新手入门</a></el-col>
          <el-col :span="4"><a href="#">API</a></el-col>
          <el-col :span="4"><a href="#">关于</a></el-col>
          <el-col :span="4"><a href="#">注册</a></el-col>
          <el-col :span="4">  <a href="#">登录</a></el-col>
        </el-row>
      </el-col>
    </el-row>
  </el-header>
</template>
