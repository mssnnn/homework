<template>
    <div class="hello" style="width: 60%;margin: 50px auto">
        <div style="margin-top: 20px">
            <el-button style="float: left" type="primary">添加员工</el-button>
            <!--      <el-button @click="toggleSelection()">取消选择</el-button>-->
        </div>

        <el-table
                ref="multipleTable"
                :data="tableData"
                tooltip-effect="dark"
                style="width: 100%"
                @selection-change="handleSelectionChange">
            <el-table-column
                    type="selection"
                    width="55">
            </el-table-column>
            <el-table-column
                    label="姓名"
                    width="130">
                <template slot-scope="scope">{{ scope.row.name }}</template>
            </el-table-column>
            <el-table-column
                    prop="phone"
                    label="手机号码"
                    width="240">
            </el-table-column>
            <el-table-column
                    prop="mail"
                    label="邮箱"
                    width="240"
                    show-overflow-tooltip>
            </el-table-column>
            <el-table-column
                    prop="job"
                    label="职务"
                    width="130"
                    show-overflow-tooltip>
            </el-table-column>
            <el-table-column
                    prop="department"
                    label="部门"
                    width="130"
                    show-overflow-tooltip>
            </el-table-column>
        </el-table>
        <div>
            <el-pagination
                    style="float: left"
                    @size-change="handleSizeChange"
                    @current-change="handleCurrentChange"
                    :current-page="pageNum"
                    :page-sizes="[3, 6, 9, 15]"
                    :page-size="pageSize"
                    layout="total, prev, pager, next,sizes, jumper"
                    :total="data.length">
            </el-pagination>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                data: [{
                    name: '王小虎1',
                    phone: 13366678903,
                    mail: '123456789@qq.com',
                    job: '部长',
                    department: '天津市滨海新区',

                }, {
                    name: '王小虎2',
                    phone: 13366678903,
                    mail: '123456789@qq.com',
                    job: '部长',
                    department: '天津市滨海新区',

                }, {
                    name: '王小虎3',
                    phone: 13366678903,
                    mail: '123456789@qq.com',
                    job: '部长',
                    department: '天津市滨海新区',

                }, {
                    name: '王小虎4',
                    phone: 13366678903,
                    mail: '123456789@qq.com',
                    job: '部长',
                    department: '天津市滨海新区',

                }, {
                    name: '王小虎5',
                    phone: 13366678903,
                    mail: '123456789@qq.com',
                    job: '部长',
                    department: '天津市滨海新区',

                }, {
                    name: '王小虎6',
                    phone: 13366678903,
                    mail: '123456789@qq.com',
                    job: '部长',
                    department: '天津市滨海新区',

                }, {
                    name: '王小虎7',
                    phone: 13366678903,
                    mail: '123456789@qq.com',
                    job: '部长',
                    department: '天津市滨海新区',

                }, {
                    name: '王小虎8',
                    phone: 13366678903,
                    mail: '123456789@qq.com',
                    job: '部长',
                    department: '天津市滨海新区',
                }],
                multipleSelection: [],
                pageNum: 1,
                pageSize: 5,
                tableData: []
            }
        },

        methods: {
            toggleSelection(rows) {
                if (rows) {
                    rows.forEach(row => {
                        this.$refs.multipleTable.toggleRowSelection(row);
                    });
                } else {
                    this.$refs.multipleTable.clearSelection();
                }
            },
            handleSelectionChange(val) {
                this.multipleSelection = val;
            },
            handleCurrentChange(){
              this.pageNum
              this.pageSize
              this.tableData
              this.data

            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
