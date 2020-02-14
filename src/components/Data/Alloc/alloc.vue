<template>
    <el-table
            :data="tableData"
            style="width: 100%">
        <el-table-column
                label="学院"
                prop="college">
        </el-table-column>
        <el-table-column
                label="性别"
                prop="sex">
        </el-table-column>
        <el-table-column
                label="优先分配的宿舍楼"
                prop="advance_Building">
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
        name: "alloc",
        props: {
            root: Boolean
        },
        data(){
            return {
                tableData: ''
            }
        },
        methods: {
            handleDelete(index, row) {
                // eslint-disable-next-line no-console
                console.log('upload',row);
                axios.post(`/deleteAlloc`,row)
                    .then(res=>{
                        // eslint-disable-next-line no-console
                        console.log('res=>',res);
                        const url = '/alloc';
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
            const url = '/alloc';
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
