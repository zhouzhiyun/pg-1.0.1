<template>
    <div class="home h-100">
        <el-container class="h-100">
            <el-aside width="200px" class="h-100" :collapse="isCollapse" >
                <el-menu default-active="1-4-1" class="el-menu-vertical-demo" 
                background-color="#545c64" text-color="#fff" active-text-color="#ffd04b"
                 @open="handleOpen" @close="handleClose" >
                    <el-menu-item index="1" style="margin-top:58px;" @click="tab='userInfo'">
                        <i class="el-icon-location"></i>
                        <span slot="title">用户信息</span>
                    </el-menu-item>
                    <el-menu-item index="2"  @click="tab='roleInfo'">
                        <i class="el-icon-menu"></i>
                        <span slot="title">角色管理</span>
                    </el-menu-item>
                    <el-menu-item index="3"  @click="tab='deviceInfo'">
                        <i class="el-icon-setting"></i>
                        <span slot="title">设备管理</span>
                    </el-menu-item>
                    <el-menu-item index="4"  @click="tab='taskInfo'">
                        <i class="el-icon-view"></i>
                        <span slot="title">任务管理</span>
                    </el-menu-item>
                </el-menu>
            </el-aside>
            <el-container class="h-100">
                <el-header style="text-align: right; font-size: 12px">
                    <span style="margin-right:10px;">王小虎</span>
                    <el-button @click="close" size="mini" type="danger">退出登录</el-button>                    
                </el-header>
                <el-main>
                    <component :is="tab"></component>
                </el-main>
                
            </el-container>
        </el-container>
    </div>
</template>

<script>
import userInfo from '../components/userInfo'
import roleInfo from '../components/roleInfo'
import deviceInfo from '../components/deviceInfo'
import taskInfo from '../components/taskInfo'
export default {
  name: 'Home',
  data () {
    return {
        isCollapse:false,
        tab:'userInfo'
    }
  },
  methods:{
      collapse(){
          if(this.isCollapse){
              this.isCollapse=false;
          }else{
              this.isCollapse=true;
          }
      },
      handleOpen(key, keyPath) {
        console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
      close(){
          console.log('ssss');
          this.$router.push({name:'Login'});
      }
  },
  components:{
      userInfo,
      roleInfo,
      deviceInfo,
      taskInfo
  }
}
</script>

<style scoped>
.el-aside{
    background-color:#545c64;
}

.el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
  }
.el-footer{
    background-color:#fafafa;
    line-height:58px;    
}
.el-menu{
    border-right:none;
}
</style>
