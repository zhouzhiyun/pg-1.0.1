<template>
  <div class="">
    <div id="btns">
      <el-button type="primary" size="mini" icon="el-icon-plus" @click="addRow($event)">增加设备</el-button>
    </div>
    <el-table
    :data="tableData"
    border
    style="width: 100%">
    <el-table-column
      fixed
      prop="date"
      label="日期">
    </el-table-column>
    <el-table-column
      prop="name"
      label="姓名">
    </el-table-column>
    <el-table-column
      prop="device"
      label="设备名称">
    </el-table-column>
    <el-table-column
      width="150"
      label="信号源">
      <template slot-scope="scope">
        <el-switch
          v-model="scope.row.signal1"
          inactive-text="信号1"
          active-color="#13ce66"
          inactive-color="#ff4949"
          active-value="true"
          inactive-value="false">
        </el-switch>
        <el-switch
          v-model="scope.row.signal2"
          inactive-text="信号2"
          active-color="#13ce66"
          inactive-color="#ff4949"
          active-value="true"
          inactive-value="false">
        </el-switch>
      </template>
    </el-table-column>
    <el-table-column
      fixed="right"
      label="操作"
      width="150">
      <template slot-scope="scope">
        <el-button @click="edit($event, scope.$index, tableData)" size="mini">编辑</el-button>
        <el-button
          @click.native.prevent="deleteRow(scope.$index, tableData)"
          type="danger"
          size="mini">
          移除
        </el-button>
      </template>
    </el-table-column>
  </el-table>

  <el-dialog
    title="提示"
    :visible.sync="dialogVisible"
    width="35%"
    :close-on-click-modal="clickModel"
    center>
    <el-form :model="editData">
      <el-form-item label="日期" :label-width="'55px'">
        <el-input :disabled="true" v-model="editData.date"></el-input>
      </el-form-item>
      <el-form-item label="姓名" :label-width="'55px'">
        <el-input v-model="editData.name"></el-input>
      </el-form-item>
      <el-form-item label="设备名称" :label-width="'55px'">
        <el-input v-model="editData.device"></el-input>
      </el-form-item>
      <el-form-item label="信号源" :label-width="'55px'">
        <template slot-scope="scope">
          <el-switch
            v-model="editData.signal1"
            inactive-text="信号1"
            active-color="#13ce66"
            inactive-color="#ff4949"
            active-value="true"
            inactive-value="false">
          </el-switch>
           <el-switch
            v-model="editData.signal2"
            inactive-text="信号2"
            active-color="#13ce66"
            inactive-color="#ff4949"
            active-value="true"
            inactive-value="false">
          </el-switch>
        </template>
      </el-form-item>
    </el-form>
    <el-row slot="footer" type="flex" justify="space-around" class="row-bg dialog-footer">
      <el-button @click="dialogVisible = false">取 消</el-button>
      <el-button type="primary" @click="changeValue">确 定</el-button>
    </el-row>
  </el-dialog>

  </div>
</template>

<script>
export default {
    data() {
      return {
        text:'',
        dialogVisible: false,
        clickModel: false,
        index:'',
        tableData: [{
          date: '2016-05-03',
          name: '王小虎',
          device: '上海',
          signal1:'true',
          signal2:'true',
        }, {
          date: '2016-05-02',
          name: '王小虎',
          device: '上海',
          signal1:'true',
          signal2:'true'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          device: '上海',
          signal1:'true',
          signal2:'true'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          device: '上海',
          signal1:'true',
          signal2:'true'
        }],
        editData:{
          date:'',
          name:'',
          device:'',
          signal1:true,
          signal2:true
        }
      }
    },
    methods: {
      deleteRow(index, rows) {
        rows.splice(index, 1);
        // console.log(rows)
      },
      edit(event, index, rows){
        let vm = this;
        vm.editData.date = rows[index].date;
        vm.editData.name = rows[index].name;
        vm.editData.device = rows[index].device;
        vm.editData.signal1 = rows[index].signal1;
        vm.editData.signal2 = rows[index].signal2;
        vm.dialogVisible = true;
        vm.index = index;
        vm.text = event.target.innerText;
      },
      changeValue(){
        let vm = this;
        if(vm.text === '编辑'){
          let index = vm.index;
          let editData = vm.editData;
          let row = vm.tableData[index];
          row.date = editData.date;
          row.name = editData.name;
          row.device = editData.device;
          row.signal1 = editData.signal1;
          row.signal2 = editData.signal2;
          vm.dialogVisible = false;
        }else if(vm.text === '增加设备'){
          vm.tableData.push(vm.editData)
        }
      },
      addRow(event){
        let date = new Date();
        let vm = this;
        vm.editData.date = null;
        vm.editData.name = null;
        vm.editData.device = null;
        vm.editData.signal1 = null;
        vm.editData.signal2 = null;
        vm.editData.date = date.toLocaleDateString();
        vm.dialogVisible = true;
        vm.text = event.target.innerText;
      }
    },
  }
</script>

<style scoped>
  #btns{
    width: 100%;
    height: 45px;
  }
</style>
