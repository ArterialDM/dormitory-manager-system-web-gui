<template>
    <el-menu :default-openeds="['1','3']">
        <el-submenu index="1">
            <template slot="title">
                <i class="el-icon-menu"></i>
                <span>学生管理</span>
            </template>
            <el-menu-item index="1-1" v-on:click="state.model='1-1'">学生入学</el-menu-item>
            <el-menu-item index="1-2" v-on:click="state.model='1-2'">学生入住</el-menu-item>
            <el-menu-item index="1-3" v-on:click="state.model='1-3'">学生维护</el-menu-item>
        </el-submenu>
        <el-submenu index="2">
            <template slot="title">
                <i class="el-icon-menu"></i>
                <span>信息查询</span>
            </template>
            <el-menu-item index="2-1" v-on:click="state.model='2-1'">学生</el-menu-item>
            <el-menu-item index="2-2" v-on:click="state.model='2-2'">宿舍楼</el-menu-item>
            <el-menu-item index="2-3" v-on:click="state.model='2-3'">宿舍</el-menu-item>
            <el-menu-item index="2-4" v-on:click="state.model='2-4'">床位</el-menu-item>
            <el-menu-item index="2-5" v-on:click="state.model='2-5'">分配策略</el-menu-item>
            <el-menu-item index="2-6" v-on:click="state.model='2-6'">进出表</el-menu-item>
        </el-submenu>
        <el-submenu index="3">
            <template slot="title">
                <i class="el-icon-menu"></i>
                <span>寝室分配</span>
            </template>
            <el-menu-item index="3-1" v-on:click="state.model='3-1'">自动分配</el-menu-item>
            <el-menu-item index="3-2" disabled>自定义分配</el-menu-item>
        </el-submenu>
        <el-submenu index="4">
            <template slot="title">
                <i class="el-icon-menu"></i>
                <span>出入登记</span>
            </template>
            <el-menu-item index="4-1" v-on:click="state.model='4-1'">学生进入</el-menu-item>
            <el-menu-item index="4-2" v-on:click="state.model='4-2'">学生离开</el-menu-item>
        </el-submenu>
    </el-menu>
</template>

<script>
    export default {
        name: 'NavMenu',
        props: {
            state: {
                model: String
            }
        },
        methods: {
        }
    }
</script>
