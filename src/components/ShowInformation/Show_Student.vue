<template>
    <el-container style="height: 400px">
        <el-aside width="300px">
            <el-main style="margin-top: -20px">
                <el-card>
                    <img src="./pic/Wendy.jpeg" class="image">
                </el-card>
            </el-main>
        </el-aside>
        <el-main>
            <el-card class="box-card">
                <div slot="header">
                    <span>学生信息</span>
                </div>
                <div style="font-size: 14px; margin-bottom: 18px;">
                    <p>学号:{{student.studentID}}</p>
                    <p>姓名:{{student.name}}</p>
                    <p>所在学院:{{student.college}}</p>
                    <p>所在宿舍床:{{student.bedID}}</p>
                </div>
            </el-card>
        </el-main>
    </el-container>
</template>

<script>
    export default {
        name: "Show_Student",
        props: {
            student: {
                studentID: String,
                name: String,
                college: String,
                bedID: String
            }
        },
        data() {
            return {
                studentTest: {
                    studentID: 2333,
                    name: 'Wendy',
                    college: '列治文山中学',
                    building: 'Korea'
                }
            };
        }
    }
</script>

<style scoped>
    .image {
        width: 100%;

        display: block;
    }

    .time {
        font-size: 13px;
        color: #999;
        float: left;
    }
    
    .button {
        padding: 0;
        float: right;
    }

    .bottom {
        margin-top: 13px;
        line-height: 12px;
    }
</style>
