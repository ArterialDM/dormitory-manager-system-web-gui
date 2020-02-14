<template>
    <div id="app">
        <el-container style="height: 850px; border: 1px solid #eee">
            <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
                <NavMenu1 v-bind:state="state"></NavMenu1>
            </el-aside>
            <el-container>
                <el-header style="text-align: right; font-size: 12px">
                    <el-dropdown>
                        <i class="el-icon-user" style="margin-right: 15px"></i>
                        <el-dropdown-menu slot="dropdown">
                            <el-dropdown-item><el-button type="text">查看账户</el-button></el-dropdown-item>
                            <el-dropdown-item><el-button type="text" @click="logout()">退出登陆</el-button></el-dropdown-item>
                        </el-dropdown-menu>
                    </el-dropdown>
                    <span>{{username}}</span>
                </el-header>
                <el-main v-if="!login">
                    <el-form  label-width="100px" class="demo-ruleForm">
                        <el-form-item label="用户名">
                            <el-input v-model.number="inputUser" autocomplete="off"></el-input>
                        </el-form-item>
                        <el-form-item>
                            <el-button type="primary" @click="check_login()">登陆</el-button>
                            <el-button @click="inputUser=''">重置</el-button>
                        </el-form-item>
                    </el-form>
                </el-main>
                <el-main v-if="login">
                    <AddStudent v-if="state.model=='1-1'"></AddStudent>
                    <StudentToLive v-if="state.model=='1-2'"></StudentToLive>
                    <UpdataStudent v-if="state.model=='1-3'"></UpdataStudent>
                    <Student v-if="state.model=='2-1'" v-bind:root="root"></Student>
                    <Building v-if="state.model=='2-2'" v-bind:root="root"></Building>
                    <Dormitory v-if="state.model=='2-3'" v-bind:root="root"></Dormitory>
                    <Bed v-if="state.model=='2-4'" v-bind:root="root"></Bed>
                    <alloc v-if="state.model=='2-5'" v-bind:root="root"></alloc>
                    <Enter_Leave v-if="state.model=='2-6'" v-bind:root="root"></Enter_Leave>
                    <AutoAlloc v-if="state.model=='3-1'"></AutoAlloc>
                    <StudentEnter v-if="state.model=='4-1'"></StudentEnter>
                    <StudentLeave v-if="state.model=='4-2'"></StudentLeave>
                </el-main>
             </el-container>
        </el-container>
    </div>
</template>

<script>

import NavMenu1 from "@/components/NavMenu/NavMenu1";
import AddStudent from "@/components/Function/AddStudent";
import StudentToLive from "@/components/Function/StudentToLive";
import UpdataStudent from "@/components/Function/UpdataStudent";
import Student from "@/components/Data/Student/Student";
import Building from "@/components/Data/Building/Building";
import Bed from "@/components/Data/Bed/Bed";
import Dormitory from "@/components/Data/Dormitory/Dormitory";
import alloc from "@/components/Data/Alloc/alloc";
import Enter_Leave from "@/components/Data/EnterLeave/Enter_Leave"
import AutoAlloc from "@/components/Function/AutoAlloc";
import StudentEnter from "@/components/Function/StudentEnter";
import StudentLeave from "@/components/Function/StudentLeave";

export default {
  name: 'app',
  components: {
      NavMenu1,
      AddStudent,
      StudentToLive,
      UpdataStudent,
      Student,
      Building,
      Dormitory,
      Bed,
      alloc,
      Enter_Leave,
      AutoAlloc,
      StudentEnter,
      StudentLeave
  },

  data: function () {
      return{
          state: {model:'1-1'},
          login: false,
          username: '未登录',
          inputUser:'',
          root:false
      }
  },

    methods: {
        check_login(){
            if(this.inputUser=='root'){
                this.username='管理员';
                this.login=true;
                this.root=true
                this.$message({
                    message: '登陆成功',
                    type: 'success'
                });
                return
            }
            if(this.inputUser=='user'){
                this.username='普通用户';
                this.login=true;
                this.$message({
                    message: '登陆成功',
                    type: 'success'
                });
                return
            }
            this.inputUser=''
            this.$message({
                message: '用户名错误',
                type: 'warning'
            });
        },
        logout(){
            this.login=false;
            this.root=false;
        }
  }
}

</script>

<style>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}

.el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
}

.el-aside {
    color: #333;
}

</style>
