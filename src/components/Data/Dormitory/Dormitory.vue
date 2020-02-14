<template>
    <el-table
            :data="tableData"
            style="width: 100%">
        <el-table-column
                label="宿舍号"
                prop="dormitoryID">
        </el-table-column>
        <el-table-column
                label="宿舍楼"
                prop="buildingID">
        </el-table-column>
        <el-table-column
                label="已入住"
                prop="hadLive">
        </el-table-column>

        <el-table-column
                label="还可以入住"
                prop="canLive">
        </el-table-column>
    </el-table>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "Dormitory",
        props: {
            root: Boolean
        },
        data() {
            return {
                tableData: ''
            }
        },
        methods: {
        },
        created: function () {
            const url = '/dormitory';
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
