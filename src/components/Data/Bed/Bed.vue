<template>
    <el-table
            :data="tableData"
            style="width: 100%">
        <el-table-column
                label="床号"
                prop="bedID">
        </el-table-column>
        <el-table-column
                label="所在宿舍楼"
                prop="buildingID">
        </el-table-column>

        <el-table-column
                label="是否已用"
                prop="can">
        </el-table-column>
    </el-table>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "Bed",
        props: {
            root: Boolean
        },
        data() {
            return {
                tableData: ''
            }
        },
        methods: {
            handleEdit(index, row) {
                // eslint-disable-next-line no-console
                console.log(index, row);
                },
            handleDelete(index, row) {
                // eslint-disable-next-line no-console
                console.log(index, row);
            }
        },
        created: function () {
            const url = '/bed';
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
