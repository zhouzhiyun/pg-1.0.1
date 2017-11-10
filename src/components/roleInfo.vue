<template>
  <div class="role">
    <div>
      <el-button type="primary" size="mini" @click="add()" icon="el-icon-plus">添加用户</el-button>
    </div>
    <el-table
      :data="tableData"
      border
      style="width: 851px;margin-top:20px;">
      <el-table-column
        fixed
        prop="username"
        label="用户名"
        width="120">
      </el-table-column>
      <el-table-column
        prop="role"
        label="角色名"
        width="120">
      </el-table-column>
      <el-table-column
        prop="power"
        label="权限"
        width="240">
      </el-table-column>
      <el-table-column
        prop="forbanden"
        label="启用/禁止"
        width="120">
      </el-table-column>      
      <el-table-column
        fixed="right"
        label="操作"
        width="250">
        <template slot-scope="scope">         
          <el-button
            size="mini"
            type="danger"
            @click="del(scope.$index)">删除</el-button>
            <el-button
            size="mini"
            type="warning" plain
            @click="change(scope.$index,scope.row)">更改密码</el-button>
          <el-button
          size="mini"
           @click="edit(scope.$index, scope.row)">编辑</el-button>
         
        </template>
      </el-table-column>
    </el-table>
    <!-- 编辑-->
    <el-dialog title="编辑" :visible.sync="dialogFormVisible">     
      <el-form ref="form" :model="form" label-width="80px">
        <el-form-item label="用户名">
          <el-input v-model="form.username"></el-input>
        </el-form-item>
        <el-form-item label="角色名">
          <el-select v-model="form.role" placeholder="请选择">
            <el-option label="超级管理员" value="超级管理员"></el-option>
            <el-option label="设备管理员" value="设备管理员"></el-option>
            <el-option label="用户管理员" value="用户管理员"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="权限">
          <el-checkbox-group v-model="form.power">
            <el-checkbox label="权限1" name="power"></el-checkbox>
            <el-checkbox label="权限2" name="power"></el-checkbox>
            <el-checkbox label="权限3" name="power"></el-checkbox>
            <el-checkbox label="权限4" name="power"></el-checkbox>
          </el-checkbox-group>
        </el-form-item>
        <el-form-item label="启用/禁止">
          <el-radio-group v-model="form.forbanden">
            <el-radio label="启用"></el-radio>
            <el-radio label="禁止"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="editSuccess">确定</el-button>
          <el-button @click="dialogFormVisible = false">取消</el-button>
        </el-form-item>
      </el-form>     
    </el-dialog>
    <!--更改密码 -->  
    <el-dialog title="更改密码" :visible.sync="dialogPsdVisible">      
      <el-form  status-icon  ref="ruleForm2" label-width="100px" class="demo-ruleForm">
        <el-form-item label="新密码" >
          <el-input type="password" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="确认密码" >
          <el-input type="password"  auto-complete="off"></el-input>
        </el-form-item>
        
        <el-form-item>
          <el-button type="primary" @click="dialogPsdVisible=false">提交</el-button>
          <el-button @click="dialogPsdVisible=false">取消</el-button>
        </el-form-item>
      </el-form>
    </el-dialog> 
  </div>
</template>

<script>
export default {
  name: 'role',
  data () {
    return {
      tableData:[
        {
          username:'王小虎',
          role:'超级管理员',
          power:['权限1','权限2'],
          forbanden:'启用'
        },
        {
          username:'王小虎',
          role:'超级管理员',
          power:['权限1','权限2'],
          forbanden:'启用'
        },
        {
          username:'王小虎',
          role:'超级管理员',
          power:['权限1','权限2'],
          forbanden:'启用'
        },
        {
          username:'王小虎',
          role:'超级管理员',
          power:['权限1','权限2'],
          forbanden:'启用'
        },
        {
          username:'王小虎',
          role:'超级管理员',
          power:['权限1','权限2'],
          forbanden:'启用'
        },
        {
          username:'王小虎',
          role:'超级管理员',
          power:['权限1','权限2'],
          forbanden:'启用'
        }
      ],
      dialogPsdVisible: false,
      dialogFormVisible: false,
      form: {
          username:'',
          role:'',
          power:[],
          forbanden:''
        },
      formLabelWidth: '120px',
      len:Number,
      text:''
    }
  },
  methods:{
    edit(index,row){
      this.text="edit";
      this.form.username=row.username;
      this.form.role=row.role;
      this.form.power=row.power;
      this.form.forbanden=row.forbanden;
      this.len=index;
      this.dialogFormVisible = true;
    },
    editSuccess(){
      let vm=this;      
      if(vm.text==="edit"){
        let len=vm.len;
        vm.tableData[len].username=vm.form.username;
        vm.tableData[len].role=vm.form.role;
        vm.tableData[len].power=vm.form.power;
        vm.tableData[len].forbanden=vm.form.forbanden;
      }else if(vm.text==="add"){
        console.log(vm.form);
        vm.tableData.push({
          username:vm.form.username,
          role:vm.form.role,
          power:vm.form.power,
          forbanden:vm.form.forbanden
        });
      }
      vm.dialogFormVisible = false;
    },
    add(){
      this.text="add";
      this.form={
        username:'',
        role:'',
        power:[],
        forbanden:''
      };    
      this.dialogFormVisible = true;
    },
    del(index){
      this.$confirm('此操作将永久删除该用户, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.tableData.splice(index,1);
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      
    },
    change(){
      this.dialogPsdVisible=true;
    }
  }
}
</script>

<style scoped>

</style>
