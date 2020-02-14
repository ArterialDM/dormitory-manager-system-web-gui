<template>
    <el-table
            :data="tableData"
            style="width: 100%">
        <el-table-column
                prop="buildingID"
                label="宿舍楼">
        </el-table-column>
        <el-table-column
                prop="student_live_count"
                label="可入住学生量">
        </el-table-column>
        <el-table-column
                prop="student_lived_count"
                label="已入住学生量">
        </el-table-column>
        <el-table-column
                prop="dormitory_have_count"
                label="可用宿舍量">
        </el-table-column>
        <el-table-column
                prop="dormitory_had_count"
                label="已用宿舍量">
        </el-table-column>
    </el-table>
</template>

<script>
    import axios from 'axios';
    
    export default {
        name: "Building",
        props: {
            root: Boolean
        },
        data:function() {
            return {
                tableData: ''
            }
        },
        created: function () {
            const url = '/building';
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
