<template>
  <div class="">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>个人信息</span>
        <el-button style="float: right; padding: 3px 0" type="text" @click="dialogFormVisible = true">更改密码</el-button>
      </div>
      <div>
        <img src="../assets/person-default.jpg" align="top" class="image"/>
        <div class="wrap">
          <div class="text item">
            <span class="item-left">用 户 名：</span>
            <span>{{userInfo.username}}</span>
          </div>
          <div class="text item">
            <span class="item-left">角 色 名：</span>
            <span>{{userInfo.role}}</span>
          </div>
          <div class="text item">
            <span class="item-left">权&nbsp;&nbsp;&nbsp;限：</span>
            <span>{{userInfo.power}}</span>
          </div>
          <div class="text item">
            <span class="item-left">启用/禁止：</span>
            <span>{{userInfo.forbanden}}</span>
          </div>
        </div>
      </div>
    </el-card>

    <!--更改密码-->
    <el-dialog title="更改密码" :visible.sync="dialogFormVisible">      
      <el-form :model="ruleForm2" status-icon :rules="rules2" ref="ruleForm2" label-width="100px" class="demo-ruleForm">
        <el-form-item label="原密码" prop="oldpsd">
          <el-input v-model.number="ruleForm2.oldpsd"></el-input>
        </el-form-item>
        <el-form-item label="新密码" prop="pass">
          <el-input type="password" v-model="ruleForm2.pass" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="确认密码" prop="checkPass">
          <el-input type="password" v-model="ruleForm2.checkPass" auto-complete="off"></el-input>
        </el-form-item>
        
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm2')">提交</el-button>
          <el-button @click="resetForm('ruleForm2')">重置</el-button>
        </el-form-item>
      </el-form>
    </el-dialog>    
  </div>
</template>

<script>
export default {
  name: 'User',
  data () {
    var checkOldpsd = (rule, value, callback) => {
      if (!value) {
        return callback(new Error('请输入原密码'));
      } else {
        if (this.ruleForm2.checkPass !== '') {
          this.$refs.ruleForm2.validateField('checkPass');
        }
        callback();
      }
      
    };
    var validatePass = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入新密码'));
      } else {
        if (this.ruleForm2.checkPass !== '') {
          this.$refs.ruleForm2.validateField('checkPass');
        }
        callback();
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请再次输入密码'));
      } else if (value !== this.ruleForm2.pass) {
        callback(new Error('两次输入密码不一致!'));
      } else {
        callback();
      }
    };
    return {
      userInfo:{
          username:'王小虎',
          role:'超级管理员',
          power:'权限1  权限2',
          forbanden:'启用'
      },
      dialogFormVisible: false,
      ruleForm2: {
        pass: '',
        checkPass: '',
        oldpsd: ''
      },
      rules2: {
        pass: [
          { validator: validatePass, trigger: 'blur' }
        ],
        checkPass: [
          { validator: validatePass2, trigger: 'blur' }
        ],
        oldpsd: [
          { validator: checkOldpsd, trigger: 'blur' }
        ]
      }
    };
  },
  methods:{
    submitForm(formName) {
      let vm=this;
      vm.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!');
        } else {
          console.log('error submit!!');
          vm.dialogFormVisible = false
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

<style scoped>
.text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 18px;
    
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both
  }

  .box-card {
    width: 480px;
  }
  .image{
    width:100px;
    height:100px;
    
  }
  .wrap{
    display:inline-block;
    min-height:100px;
    margin-left:10px;
    
  }
  .item-left{
    width:80px;
    display:inline-block;
    text-align:justify;
    text-align-last:justify;
  }
  
</style>
