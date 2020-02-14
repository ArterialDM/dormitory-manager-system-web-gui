<template>
    <el-container>
        <el-main>
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="学生学号">
                    <el-input v-model="form.studentID" v-bind:suffix-icon="suffix_icon" @blur="Search_Student"></el-input>
                </el-form-item>
                <div>
                    <p v-if="!haveShow">请输入需要修改的学生的学号</p>
                </div>
                <div v-if="haveShow">
                    <el-form-item label="学生姓名">
                        <el-input v-model="form.name"></el-input>
                    </el-form-item>
                    <el-form-item label="所在学院">
                        <el-select v-model="form.college" placeholder="请选择所在学院">
                            <el-option label="计算机工程学院" value="computer"></el-option>
                            <el-option label="外国语学院" value="language"></el-option>
                            <el-option label="经济学院" value="economy"></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="报道时间">
                        <el-col :span="11">
                            <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" default-value="form.date1" style="width: 100%;"></el-date-picker>
                        </el-col>
                        <el-col class="line" :span="2">-</el-col>
                        <el-col :span="11">
                            <el-time-picker placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="是否入住">
                        <el-switch v-model="form.live"></el-switch>
                    </el-form-item>
                    <el-form-item label="政治面貌">
                        <el-radio-group v-model="form.politics">
                            <el-radio label="群众"></el-radio>
                            <el-radio label="团员"></el-radio>
                            <el-radio label="党员"></el-radio>
                            <el-radio label="其他党派人士"></el-radio>
                        </el-radio-group>
                    </el-form-item>
                    <el-form-item label="性别">
                        <el-radio-group v-model="form.sex">
                            <el-radio label="男"></el-radio>
                            <el-radio label="女"></el-radio>
                        </el-radio-group>
                    </el-form-item>
                    <el-form-item label="备注" >
                        <el-input type="textarea" :rows="9" v-model="form.desc" ></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" @click="onSubmit">保存修改</el-button>
                    </el-form-item>
                </div>
            </el-form>
        </el-main>
    </el-container>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "UpdataStudent",
        data() {
            return {
                suffix_icon: 'el-icon-edit',
                haveShow: false,
                form: {
                    studentID: '',
                    name: '',
                    date1: '',
                    date2: '',
                    live: false,
                    politics: '',
                    sex: '',
                    desc: '',
                    time1: '',
                    time2: ''
                }
            }
        },
        methods: {
            Search_Student(){
                this.suffix_icon='el-icon-loading';
                if(this.form.studentID==''){
                    this.suffix_icon='el-icon-edit';
                    this.haveShow=false;
                    return;
                }
                // eslint-disable-next-line no-console
                console.log('upload',this.form);
                axios.post(`/searchStudent`,this.form)
                    .then(res=>{
                        // eslint-disable-next-line no-console
                        console.log('res=>',res);
                        if(res.data.name==''){
                            this.haveShow=false;
                            this.suffix_icon='el-icon-error';
                            this.$message({
                                message: '查不到此学生信息',
                                type: 'warning'
                            });
                            return
                        }
                        this.form=res.data;
                        this.form.date1=new Date(parseInt(res.data.time1));
                        this.form.date2=new Date(parseInt(res.data.time2));
                        this.suffix_icon='el-icon-success';
                        this.$message({
                            message: '查询学生信息成功',
                            type: 'success'
                        });
                        this.haveShow=true;
                    });
             },
             onSubmit() {
                 this.form.time1=this.form.date1.getTime();
                 this.form.time2=this.form.date2.getTime();
                 // eslint-disable-next-line no-console
                 console.log('upload',this.form);
                 axios.post(`/updateStudent`,this.form)
                     .then(res=>{
                         // eslint-disable-next-line no-console
                         console.log('res=>',res);
                         if(res.data.result=='fail'){
                             this.$message({
                                 message: '添加失败',
                                 type: 'warning'
                             });
                         }
                         if(res.data.result=='success'){
                             this.$message({
                                 message: '添加成功',
                                 type: 'success'
                             });
                         }
                     });
             }
         }
     }
</script>

<style scoped>

</style>
