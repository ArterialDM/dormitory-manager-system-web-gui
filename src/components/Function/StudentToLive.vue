<template>
    <el-container>
        <el-main>
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="学生学号">
                    <el-input v-model="form.studentID" v-bind:suffix-icon="suffix_icon1" @blur="Search_Student"></el-input>
                </el-form-item>
                <div>
                    <p v-if="!haveShow">请输入需要分配床位的学生的学号</p>
                </div>
                <div v-if="haveShow">
                    <el-form-item label="床号">
                        <el-input v-model="form.bedID" v-bind:suffix-icon="suffix_icon2" @blur="Search_Bed"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" @click="onSubmit">确认分配信息</el-button>
                    </el-form-item>
                </div>
            </el-form>
        </el-main>
    </el-container>
</template>

<script>
    import axios from 'axios';
    
    export default {
        name: "StudentToLive",
        data(){
            return{
                suffix_icon1: 'el-icon-edit',
                suffix_icon2: 'el-icon-edit',
                haveShow: false,
                form:{
                    studentID: '',
                    bedID: ''
                }
            }
        },
        methods:{
            Search_Student(){
                this.suffix_icon1='el-icon-loading';
                this.form.bedID='';
                if(this.form.studentID==''){
                    this.suffix_icon1='el-icon-edit';
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
                                message: '不存在此学生',
                                type: 'warning'
                            });
                            return
                        }
                        this.suffix_icon1='el-icon-success';
                        this.$message({
                            message: '存在学生信息',
                            type: 'success'
                        });
                        this.haveShow=true;
                    });
            },
            Search_Bed(){
                this.suffix_icon2='el-icon-loading';
                if(this.form.bedID==''){
                    this.suffix_icon2='el-icon-edit';
                    return;
                }
                // eslint-disable-next-line no-console
                console.log('upload',this.form);
                axios.post(`/canUseBed`,this.form)
                    .then(res=>{
                        // eslint-disable-next-line no-console
                        console.log('res=>',res);
                        if(res.data.result=='fail'){
                            this.suffix_icon2='el-icon-error';
                            this.$message({
                                message: '此床不可用',
                                type: 'warning'
                            });
                            return
                        }
                        this.suffix_icon2='el-icon-success';
                        this.$message({
                            message: '此床可以用',
                            type: 'success'
                        });
                    });
            },
            onSubmit(){
                // eslint-disable-next-line no-console
                console.log('upload',this.form);
                axios.post(`/studentAddBed`,this.form)
                    .then(res=>{
                        // eslint-disable-next-line no-console
                        console.log('res=>',res);
                        if(res.data.result=='fail'){
                            this.$message({
                                message: '分配床失败',
                                type: 'warning'
                            });
                            return
                        }
                        if(res.data.result=='success'){
                            this.$message({
                                message: '分配床成功',
                                type: 'success'
                            });
                            return
                        }
                    });
            }
    }
</script>

<style scoped>

</style>
