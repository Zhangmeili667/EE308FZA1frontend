<template>
    <div>
        <el-container>
            <!-- 标题 -->
            <el-header>
                张敏慧的通讯录
            </el-header>

            <!-- 页面主体 -->
            <el-main>
                
            <!--搜索表单-->
            <el-form :inline="true" :model="searchForm" class="demo-form-inline">
            <el-form-item label="姓名">
                <el-input
                v-model="searchForm.name"
                placeholder="请输入姓名"
                ></el-input>
            </el-form-item>
            <el-form-item label="性别">
                <el-select v-model="searchForm.gender" placeholder="请选择">
                <el-option label="男" value="1"></el-option>
                <el-option label="女" value="2"></el-option>
                </el-select>
            </el-form-item>

            <!-- 查询和清空按钮 -->
            <el-form-item>
                <el-button type="primary" @click="onSubmit">查询</el-button>
                <el-button type="info" @click="clear">清空</el-button>
            </el-form-item>

            <!-- 添加人员按钮 -->
            <el-form-item>
            <el-button 
            style="float: center" type="primary"
            @click="dialogFormVisible = true; contact = {id: '',name: '',number: '',gender:''}"
            >
            添加联系人
            </el-button>
            </el-form-item>

            </el-form>

            

            <!-- 表格内容 -->
            <el-table :data="tableData" border>
                <el-table-column prop="name" label="姓名" width="140">
                </el-table-column>
                <el-table-column prop="number" label="号码" width="200">
                </el-table-column>
                <el-table-column prop="gender" label="性别" width="100">
                    <template slot-scope="scope">
                        <span>
                        {{scope.row.gender == "1" ? "男" : "女"}}</span>
                    </template>
                </el-table-column>
                <el-table-column prop="createTime" label="创建时间" width="200">
                </el-table-column>
                <el-table-column prop="updateTime" label="更新时间" width="200">
                </el-table-column>

                <!-- 删除和编辑按钮 -->
                <el-table-column  label="操作" width="200">
                    <template slot-scope="scope">
                        <el-button type="primary" icon="el-icon-edit" circle
                        @click="update(scope.row.id)">edit</el-button>
                        <el-button type="danger" icon="el-icon-delete" circle
                        @click="deleteByID(scope.row.id)">delete</el-button>
                    </template>
                </el-table-column>
            </el-table>

            <!--对话框表单-->
           <el-dialog ref="form" title="编辑联系人" :visible.sync="dialogFormVisible" width="30%">
           <el-form ref="form" :model="contact" label-width="80px" size="mini">

           <el-form-item label="姓名">
               <el-input v-model="contact.name"></el-input>
           </el-form-item>

           <el-form-item label="性别" >
                <el-select v-model="contact.gender" placeholder="请选择" style="width:100%" >
                    <el-option
                    v-for="item in genderList"
                    :key="item.value"
                    :label="item.name"
                    :value="item.id"
                    />
                </el-select>
          </el-form-item>

            <el-form-item label="电话号码">
            <el-input v-model="contact.number"></el-input>
            </el-form-item>

        <el-form-item>
          <el-button type="primary" @click="add()">提交</el-button>
          <el-button @click="dialogFormVisible = false">取消</el-button>
        </el-form-item>

        </el-form>        
         </el-dialog>
            

            <!-- 分页    -->
            <!-- <el-pagination
                background layout="total, sizes,prev, pager, next,jumper"
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :total="1000">
            </el-pagination> -->

            </el-main>

        </el-container>

    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            tableData:[],
            searchForm:{
                        name:"",
                        gender:""
                       },
            contact:{
                        id:"",
                        name:"",
                        number:"",
                        gender:"",
                    },
            genderList:[{id: 1,name: "男"},{id: 2,name: "女"}],
            dialogFormVisible:false,
            
            }

        },
    methods:{
        init(){
            axios.get("http://localhost:7000/contacts").then((result) =>{
            this.tableData=result.data.data;
            });
        },
        onSubmit(){
            axios.get("http://localhost:7000/searchByName?name="+this.searchForm.name+"&gender="+this.searchForm.gender).then((result) =>{
            this.tableData=result.data.data;
            });
        },
        clear(){
            this.init();
            this.searchForm.name="";
            this.searchForm.gender="";
        },
        // handleSizeChange(val){
        //     alert("每页记录数变化"+val);
        // },
        // handleCurrentChange(val){
        //     alert("页码发生变化"+val);
        // },
        add(){
            if(this.contact.id){
                axios.post("http://localhost:7000/updateContact", this.contact).then((result) =>{
                this.tableData=result.data.data;
                this.init();
                });
            }
            else{
                axios.post("http://localhost:7000/contacts", this.contact).then((result) =>{
                this.tableData=result.data.data;
                this.init();    
                });
            }
            
            
        },
        deleteByID(id){
            axios.delete("http://localhost:7000/contacts/"+id).then((result) =>{
            this.tableData=result.data.data;
            this.init();
            });
        },
        searchByID(id){
            axios.get("http://localhost:7000/contacts/"+id).then((result) =>{
            if (result.data.code == 1) {
                this.contact=result.data.data;
            }
            });
        },
        update(id){
            this.searchByID(id);
            this.dialogFormVisible = true;
        },
        

    },
    mounted(){
        //发送异步请求，获取数据
        this.init();
    }

}
</script>

<style>
   .el-header {
    background-color: #c2e2e3;
    color: #333;
    text-align: center;
    line-height: 60px;
    font-size:40px;
  }
  .el-main {
    background-color: #e2efec;
    color: #333;
    text-align: center;
  }
</style>