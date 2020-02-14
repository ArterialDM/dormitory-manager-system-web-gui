<template>
    <el-container>
        <el-main>
            <Show_Student v-if="haveShow" v-bind:student="student"></Show_Student>
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="学生学号"><el-input v-model="form.studentID" v-bind:suffix-icon="suffix_icon" @blur="Search_Student"></el-input>
                </el-form-item>
                <el-form-item label="宿舍楼">
                    <el-select v-model="form.building" placeholder="请选择进入的宿舍楼">
                        <el-option label="C17" value="C17"></el-option>
                        <el-option label="C18" value="C18"></el-option>
                        <el-option label="C19" value="C19"></el-option>
                        <el-option label="C20" value="C20"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item label="进入时间">
                    <el-col :span="11">
                        <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
                    </el-col>
                    <el-col class="line" :span="2">-</el-col>
                    <el-col :span="11">
                        <el-time-picker placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
                    </el-col>
                </el-form-item>
                <el-form-item label="备注" >
                    <el-input type="textarea" :rows="1" v-model="form.desc" ></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit">创建登记</el-button>
                </el-form-item>
            </el-form>
        </el-main>
    </el-container>
</template>

<script>
    import Show_Student from "@/components/ShowInformation/Show_Student";
    import axios from 'axios';

    export default {
        name: "StudentEnter",
        components: {
            Show_Student
        },
        data() {
            return {
                suffix_icon: 'el-icon-edit',
                haveShow: false,
                form: {
                    studentID: '',
                    building: '',
                    date1: '',
                    date2: '',
                    desc: ''
                },
                student: {
                    studentID: '',
                    name: '',
                    college: '',
                    bedID: ''
                }
            }
        },
        methods: {
            onSubmit() {
                // eslint-disable-next-line no-console
                console.log(this.form);
                axios.post(`/addStudentEnter`, this.form)
                    .then(res => {
                        // eslint-disable-next-line no-console
                        console.log('res=>', res);
                        if (res.data.result == 'success') {
                            this.$message({
                                message: '添加记录成功',
                                type: 'success'
                            });

                        }
                        if (res.data.result == 'fail') {
                            this.$message({
                                message: '添加记录失败',
                                type: 'warning'
                            });
                        }
                    })

            },
            Search_Student() {
                this.suffix_icon = 'el-icon-loading'
                if (this.form.studentID == '') {
                    this.suffix_icon = 'el-icon-edit';
                    this.haveShow = false;
                    return;
                }
                // eslint-disable-next-line no-console
                console.log('upload', this.form);
                axios.post(`/searchStudent`, this.form)
                    .then(res => {
                        // eslint-disable-next-line no-console
                        console.log('res=>', res);
                        if (res.data.name == '') {
                            this.haveShow = false;
                            this.suffix_icon = 'el-icon-error';
                            this.$message({
                                message: '查不到此学生信息',
                                type: 'warning'
                            });
                            return
                        }
                        this.student = res.data;
                        this.haveShow = true;
                        this.suffix_icon = 'el-icon-success';
                        this.$message({
                            message: '查询学生信息成功',
                            type: 'success'
                        });
                    })
            }
        }
    }
</script>

<style scoped>

</style>
