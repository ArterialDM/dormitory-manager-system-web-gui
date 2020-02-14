<template>
    <el-table
            :data="tableData"
            style="width: 100%" >
        <el-table-column
                prop="studentID"
                label="学号"
                width="180">
        </el-table-column>
        <el-table-column
                prop="action"
                label="行为"
                width="160">
        </el-table-column>
        <el-table-column
                prop="buildingID"
                label="宿舍楼">
        </el-table-column>
        <el-table-column
                prop="time"
                label="时间">
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
        name: "Enter_Leave",
        props: {
            root: Boolean
        },
        data:function() {
            return {
                tableData: '',
            }
        },
        methods: {
            handleDelete(index, row) {
                // eslint-disable-next-line no-console
                console.log(index, row);
                // eslint-disable-next-line no-console
                console.log('upload',row);
                axios.post(`/deleteEnterLeave`,row)
                    .then(res=>{
                        // eslint-disable-next-line no-console
                        console.log('res=>',res);
                        const url = '/enterLeave';
                        axios.get(url).then(
                            response => {
                                this.info=response;
                                this.tableData=this.info.data;
                            }
                        )
                    });
            },
        },
        created: function () {
            const url = '/enterLeave';
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
