<template>
    <el-container>
        <el-main>
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="所在学院">
                    <el-select v-model="form.college" placeholder="请选择所在学院">
                        <el-option label="计算机工程学院" value="computer"></el-option>
                        <el-option label="外国语学院" value="language"></el-option>
                        <el-option label="经济学院" value="economy"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item label="性别">
                    <el-select v-model="form.sex" placeholder="请选择性别">
                        <el-option label="男" value="男"></el-option>
                        <el-option label="女" value="女"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit">推荐宿舍</el-button>
                </el-form-item>
            </el-form>
            <p v-if="showAuto">你获得的推荐的床号是{{bedID}}</p>
        </el-main>
    </el-container>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "AutoAlloc",
        data(){
            return {
                form: {
                    college: '',
                    sex: ''
                },
                showAuto: false,
                bedID: ''

            }
        },
        methods: {
            onSubmit(){
                // eslint-disable-next-line no-console
                console.log('upload',this.form);
                axios.post(`/autoAlloc`,this.form)
                    .then(res=>{
                        // eslint-disable-next-line no-console
                        console.log('res=>',res);
                        if(res.data.bedID==''){
                            this.$message({
                                message: '推荐失败',
                                type: 'warning'
                                });
                        }else {
                            this.$message({
                                message: '获得推荐成功',
                                type: 'success'
                            });
                            this.bedID=res.data.bedID;
                            this.showAuto=true;
                        }
                    })
            }
        }
    }
</script>

<style scoped>

</style>
