<template>
  <div class="login">
    <el-card class="box-card">
      <div slot="header" class="clearfix" style="text-align:center;">
        <span>权限管理</span>
      </div>
      <el-form :model="ruleForm2" status-icon :rules="rules2" ref="ruleForm2" label-width="100px" class="demo-ruleForm">
        <el-form-item label="用户名" prop="age" :label-width="'100px'">
          <el-input v-model.number="ruleForm2.age"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="pass" :label-width="'100px'">
          <el-input type="password" v-model="ruleForm2.pass" auto-complete="off"></el-input>
        </el-form-item>
        
        
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm2')">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
  export default {
    name:'Login',
    data() {
      var checkAge = (rule, value, callback) => {
        if (!value) {
          return callback(new Error('用户名不能为空'));
        } setTimeout(() => {
          callback();          
        }, 1000);
        
      };
      var validatePass = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('密码不能为空'));
        } else {
          if (this.ruleForm2.age !== '') {
            this.$refs.ruleForm2.validateField('age');
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
        ruleForm2: {
          pass: '',
          checkPass: '',
          age: ''
        },
        rules2: {
          pass: [
            { validator: validatePass, trigger: 'blur' }
          ],
          checkPass: [
            { validator: validatePass2, trigger: 'blur' }
          ],
          age: [
            { validator: checkAge, trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$router.push({name:'Home'});
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      }
    }
  }
</script>

<style scoped>
.box-card{
  width:450px;
  height:320px;
  position:absolute;
  top:0;
  left:0;
  right:0;
  bottom:0;
  margin:auto;
}

</style>
