<template>

  <div>
    <Top/>

  </div>
  <div style="display:flex;flex-wrap: wrap;height: 100%">
    <Aside/>

      <div style="display: flex;width: 87%;flex-direction: column">
        <div style="width: 100%">
        <el-badge :value="application" class="item" style="margin-left: 68%;margin-top: 3%;cursor:pointer;" @click="dealClick">
          <el-icon :size="25"><Bell /></el-icon>
        </el-badge>
        </div>
    <el-table
        :data="tableData"
        :default-sort="{ prop: 'date', order: 'descending' }"
        style="width: 60%;margin-left: 10%;"
    >
      <el-table-column prop="identity" label="身份"  width="180" />
      <el-table-column prop="name" label="昵称" width="180" />
      <el-table-column prop="registerTime" label="注册日期" sortable/>
      <el-table-column label="状态" width="180" >
        <template #default="scope">
      <el-switch
          v-model="scope.row.status"
          class="ml-2"
          style="--el-switch-on-color: #13ce66; --el-switch-off-color: #ff4949"
          @change="change(scope.$index)"
      />
        </template>
        </el-table-column>
    </el-table>

        <el-pagination
            :currentPage="currentPage4"
            :page-size="pageSize4"
            :page-sizes="[5, 10, 15, 20]"
            layout="total, sizes, prev, pager, next, jumper"
            :total="total"
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            style="padding-left: 25%;padding-top: 22px"
        />

        <el-dialog
            v-model="dialogVisible"
            title="提示"
            width="30%"
        >
          <span style="font-size: 16px;letter-spacing: 1px">是否确认修改用户状态</span>
          <template #footer>
      <span class="dialog-footer">
        <el-button @click="rollbackModify">取消</el-button>
        <el-button type="primary" @click="dialogVisible = false"
        >确定</el-button
        >
      </span>
          </template>
        </el-dialog>




      </div>

    <el-dialog
        v-model="centerDialogVisible"
        title="产品供方申请"
        width="30%"
        align-center
    >
      <el-form
          label-width="100px"
          :model="userForm"
          style="max-width: 460px"
      >
        <el-form-item label="昵称">
          {{userForm.name}}
        </el-form-item>
        <el-form-item label="证明文件">
        </el-form-item>
        <el-form-item label="说明">
          {{userForm.text}}
        </el-form-item>
      </el-form>



      <template #footer>
      <span class="dialog-footer">
        <el-button @click="centerDialogVisible = false">拒绝</el-button>
        <el-button type="info" @click="centerDialogVisible = false">忽略</el-button>
        <el-button type="primary" @click="centerDialogVisible = false">同意</el-button>
      </span>
      </template>
    </el-dialog>

  </div>

</template>

<script>
import Aside from '@/components/Aside.vue'
import Top from '@/components/Top.vue'
export default {
  name: "UserView",
  components:{
    Aside,
    Top
  },
  data(){
    return{
      currentPage4:0,
      pageSize4:0,
      total:0,
      confirmIndex:0,
      centerDialogVisible:false,
      application:0,
      userForm:{
        name:"",
        file:"",
        text:""
      },
      dialogVisible:false,
      tableData:[
        {
          identity:'普通用户',
          name:'张三',
          registerTime:'2022-10-11',
          status:true
        },{
          identity:'产品供方',
          name:'李四',
          registerTime:'2022-10-12',
          status:false
        },
      ]
    }
  },
  methods:{
    handleSizeChange(){
      alert(1)
    },handleCurrentChange(){

    },dealClick(){
      this.centerDialogVisible = true
    },change(index){
      this.dialogVisible = true
      this.confirmIndex = index;
    },rollbackModify(){
      this.dialogVisible = false
      this.tableData[this.confirmIndex].status = !this.tableData[this.confirmIndex].status
    }
  }
}
</script>

<style scoped>

</style>