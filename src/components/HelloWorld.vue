<template>
    <div class="hello" style="width: 60%;margin: 50px auto">
        <div style="margin-top: 20px">
            <el-button style="float: left" type="primary" @click="dialogFormVisible = true">添加员工</el-button>
            <!--      <el-button @click="toggleSelection()">取消选择</el-button>-->
        </div>
        <el-dialog title="添加员工" :visible.sync="dialogFormVisible">
            <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
                <el-divider content-position="left"></el-divider>
                <el-form-item label="基本信息"></el-form-item>
                <el-row>
                    <el-row>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="中文名" prop="name">
                                <el-input v-model="ruleForm.name" placeholder="请输入" style="width:140%;"></el-input>
                            </el-form-item>
                        </el-col>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="登录手机号" prop="telephone">
                                <el-input v-model="ruleForm.telephone" style="width:150%;"></el-input>
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <el-row>
                        <el-col :offset="2" :span="18">
                            <el-form-item label="所属部门" prop="department">
                                <el-input v-model="ruleForm.department" style="width:116%;"></el-input>
                            </el-form-item>
                        </el-col>
                    </el-row>
                </el-row>
                <el-form-item label="其他信息▲"></el-form-item>
                <el-row>
                    <el-row>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="员工ID" prop="id">
                                <el-input placeholder="请输入" style="width:150%;"></el-input>
                            </el-form-item>
                        </el-col>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="性别" prop="region">
                                <el-select v-model="sizeForm.region" style="width:150%;" placeholder="请选择">
                                    <el-option label="男" value="man"></el-option>
                                    <el-option label="女" value="woman"></el-option>
                                </el-select>
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <el-row>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="英文名" prop="englishname">
                                <el-input placeholder="请输入" style="width:150%;"></el-input>
                            </el-form-item>
                        </el-col>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="邮箱" prop="email">
                                <el-input placeholder="请输入" style="width:150%;"></el-input>
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <el-row>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="职务" prop="job">
                                <el-input placeholder="请输入" style="width:150%;"></el-input>
                            </el-form-item>
                        </el-col>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="秘书" prop="secretary">
                                <el-input placeholder="请输入" style="width:150%;"></el-input>
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <el-row>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="座机" prop="phone">
                                <el-input placeholder="请输入" style="width:150%;"></el-input>
                            </el-form-item>
                        </el-col>
                        <el-col :offset="2" :span="8">
                            <el-form-item label="办公地址" prop="address">
                                <el-input placeholder="请输入" style="width:150%;"></el-input>
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <el-row>
                        <el-col :offset="2" :span="18">
                            <el-form-item label="备注" prop="desc">
                                <el-input type="textarea" placeholder="不超过200字" style="width:116%;"></el-input>
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <el-form-item>
                        <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
                        <el-button @click="resetForm('ruleForm')">重置</el-button>
                    </el-form-item>
                </el-row>
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button type="primary" @click="dialogFormVisible = false">保 存</el-button>
                <el-button @click="dialogFormVisible = false">取 消</el-button>
            </div>
        </el-dialog>
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
                    prop="name"
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
                ruleForm: {
                    name: '',
                    telephone: '',
                    department: '',
                },
                rules: {
                    name: [
                        {required: true, message: '请输入中文名', trigger: 'blur'},
                        {min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur'}
                    ],
                    telephone: [
                        {required: true, message: '请选择活动区域', trigger: 'change'}
                    ],
                    department: [
                        {required: true, message: '请选择活动区域', trigger: 'change'}
                    ]
                },
                form: {
                    name: '',
                    telephone: '',
                    department: ''
                },
                sizeForm: {
                    region: ''
                },
                dialogFormVisible: false,
                formLabelWidth: '120px',
                multipleSelection: [],
                pageNum: 1,
                pageSize: 3,
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
            handleCurrentChange(pageNumber) {
                alert(this.pageNum +  '_' + this.pageSize +  '_' + pageNumber)
                this.tableData = []
                var start = (pageNumber - 1) * this.pageSize
                var end = start + this.pageSize
                this.data.forEach((item, index) => {
                    if (start <= index && end > index) {
                        this.tableData.push(item)
                    }
                })
            },
            handleSizeChange: function (size) {
                this.pageSize = size
                var start = (this.pageNum - 1) * this.pageSize
                var end = start + this.pageSize
                this.data.forEach((item, index) => {
                    if (start <= index && end > index) {
                        this.tableData.push(item)
                    }
                })
            },
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        alert('submit!');
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
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
