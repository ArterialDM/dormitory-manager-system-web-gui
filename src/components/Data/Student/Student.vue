<template>
    <el-table
            :data="tableData"
            style="width: 100%">
        <el-table-column
                prop="studentID"
                label="学号"
                width="180">
        </el-table-column>
        <el-table-column
                prop="name"
                label="姓名"
                width="160">
        </el-table-column>
        <el-table-column
                prop="college"
                label="学院">
        </el-table-column>
        <el-table-column
                prop="bedID"
                label="床号">
        </el-table-column>
        <el-table-column
                align="right">
            <template slot-scope="scope">
                <el-button
                        size="mini"
                        type="danger"
                        v-if="root"
                        @click="handleDelete(scope.$index, scope.row)">删除</el-button>
            </template>
        </el-table-column>
    </el-table>
</template>

<script>
    import axios from 'axios';
    
    export default {
        name: "Student",
        props: {
            root: Boolean
        },
        data:function() {
            return {
                tableData: ''
            };
        },
        methods: {
            handleDelete(index, row) {
                // eslint-disable-next-line no-console
                console.log('upload',row);
                axios.post(`/deleteStudent`,row)
                    .then(res=>{
                        // eslint-disable-next-line no-console
                        console.log('res=>',res);
                        const url = '/student';
                        axios.get(url).then(
                            response => {
                                this.info=response;
                                this.tableData=this.info.data;
                            }
                        )
                    });
            }
        },
        created: function () {
            const url = '/student';
            axios.get(url).then(
                response => {
                    this.info=response;
                    this.tableData=this.info.data;
                }
            )
        }
    }
</script>

<style scoped>

</style>
