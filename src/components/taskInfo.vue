<template>
  <div class="">
    <div id="btns">
      <el-button type="primary" size="mini" icon="el-icon-plus" @click="addRow($event)">增加任务</el-button>
    </div>
    <el-table
    :data="tableData"
    style="width: 100%">
    <el-table-column type="expand">
      <template slot-scope="props">
        <el-form label-position="left" inline id="form">
          <el-form-item label="任务名称" :label-width="'90px'">
            <span style="color:#99a9bf;">{{ props.row.name }}</span>
          </el-form-item>
          <el-form-item label="显示屏名称" :label-width="'90px'">
            <span style="color:#99a9bf;">{{ props.row.display }}</span>
          </el-form-item>
          <el-form-item label="信号源名称" :label-width="'90px'">
            <span style="color:#99a9bf;">{{ props.row.signal }}</span>
          </el-form-item>
          <el-form-item label="任务描述" :label-width="'90px'">
            <span style="color:#99a9bf;">{{ props.row.desc }}</span>
          </el-form-item>
          <el-form-item label="开始时间" :label-width="'90px'">
            <span style="color:#99a9bf;">{{ props.row.startTime }}</span>
          </el-form-item>
          <el-form-item label="结束时间" :label-width="'90px'">
            <span style="color:#99a9bf;">{{ props.row.endTime }}</span>
          </el-form-item>
        </el-form>
      </template>
    </el-table-column>
    <el-table-column
      label="创建时间"
      prop="date">
    </el-table-column>
    <el-table-column
      label="任务名称"
      prop="name">
    </el-table-column>
    <el-table-column
      label="显示屏名称"
      prop="display">
    </el-table-column>
    <el-table-column fixed="right" label="操作" width="150">
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit($event, scope.$index, scope.row)">编辑</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.$index, tableData)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>

  <el-dialog
    title="提示"
    :visible.sync="dialogVisible"
    width="37%"
    :close-on-click-modal="clickModel"
    center>
    <el-form :model="editData" label-position="left">
      <el-form-item label="日期" :label-width="'90px'">
        <el-input :disabled="true" v-model="editData.date"></el-input>
      </el-form-item>
      <el-form-item label="任务名称" :label-width="'90px'">
        <el-input v-model="editData.name" auto-complete="off"></el-input>
      </el-form-item>
      <el-form-item label="任务描述" :label-width="'90px'">
        <el-input type="textarea" :rows="2" v-model="editData.desc" auto-complete="off"></el-input>
      </el-form-item>
      <el-form-item label="显示屏名称" :label-width="'90px'">
        <el-input v-model="editData.display" auto-complete="off"></el-input>
      </el-form-item>
      <el-form-item label="信号源名称" :label-width="'90px'">
        <el-input v-model="editData.signal" auto-complete="off"></el-input>
      </el-form-item>
      <el-time-select
        placeholder="起始时间"
        v-model="editData.startTime"
        :picker-options="{
          start: '09:00',
          step: '00:5',
          end: '18:00'
        }">
      </el-time-select>
      <el-time-select
        placeholder="结束时间"
        v-model="editData.endTime"
        :picker-options="{
         start: '09:00',
          step: '00:5',
          end: '18:00',
          minTime: editData.startTime
        }">
      </el-time-select>
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
        index: '',
        tableData: [{
          date: '2017/11/08',
          name: '好滋好味鸡蛋仔',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          display: '上海市普陀区真北路',
          signal: '王小虎夫妻店',
          startTime: '8:30',
          endTime: '9:30'
        }, {
          date: '2017/11/08',
          name: '好滋好味鸡蛋仔',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          display: '上海市普陀区真北路',
          signal: '王小虎夫妻店',
          startTime: '8:30',
          endTime: '9:30'
        }, {
          date: '2017/11/08',
          name: '好滋好味鸡蛋仔',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          display: '上海市普陀区真北路',
          signal: '王小虎夫妻店',
          startTime: '8:30',
          endTime: '9:30'
        }, {
          date: '2017/11/08',
          name: '好滋好味鸡蛋仔',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          display: '上海市普陀区真北路',
          signal: '王小虎夫妻店',
          startTime: '8:30',
          endTime: '9:30'
        }],
        editData:{
          date:'',
          name: '',
          desc: '',
          display: '',
          signal: '',
          startTime: '',
          endTime: ''
        }
      }
    },
    methods: {
      handleEdit(event, index, row){
        // console.log(row)
        let vm = this;
        vm.index = index;
        vm.dialogVisible = true;
        vm.editData.date = row.date;
        vm.editData.name = row.name;
        vm.editData.desc = row.desc;
        vm.editData.display = row.display;
        vm.editData.signal = row.signal;
        vm.editData.startTime = row.startTime;
        vm.editData.endTime = row.endTime;
        vm.text = event.target.innerText;
      },
      handleDelete(index, rows){
        rows.splice(index, 1);
      },
      changeValue(){
        let vm = this;
        if(vm.text === '编辑'){
          let index = vm.index;
          let editData = vm.editData;
          let row = vm.tableData[index];
          row.date = editData.date;
          row.name = editData.name;
          row.desc = editData.desc;
          row.display = editData.display;
          row.signal = editData.signal;
          row.startTime = editData.startTime;
          row.endTime = editData.endTime;
        }else if(vm.text === '增加任务'){
          vm.tableData.push(vm.editData)
        }
        vm.dialogVisible = false;
      },
      addRow(event){
        let date = new Date();
        let vm = this;
        vm.editData.name = null;
        vm.editData.desc = null;
        vm.editData.display = null;
        vm.editData.signal = null;
        vm.editData.startTime = null;
        vm.editData.endTime = null;
        vm.editData.date = date.toLocaleDateString();
        vm.dialogVisible = true;
        vm.text = event.target.innerText;
      }
    }
  }
</script>

<style scoped>
  #form{
    font-size: 0;
  }
  #form label{
    width: 90px !important;
    color: #99a9bf;
  }
  #form .el-form-item{
    margin-right: 0;
    margin-bottom: 0;
    width: 50%;
  }
  #btns{
    width: 100%;
    height: 45px;
  }
</style>
