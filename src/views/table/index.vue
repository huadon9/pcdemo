<template>
  <div class="app-container">
    <el-table
      v-loading="listLoading"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row>
      <el-table-column align="center" label="样品号" width="95">
        <template slot-scope="scope">
          {{ scope.row.title }}
        </template>
      </el-table-column>
      <el-table-column label="样品位置">
        <template slot-scope="scope">
          {{ scope.row.address }}<img class="min-img" src="@/assets/pic.png"/>
        </template>
      </el-table-column>
      <el-table-column label="异常提醒" width="190" align="center">
        <template slot-scope="scope">
          <span :class="{handle: scope.row.warn != '已归还'}">{{ scope.row.warn }}</span>
        </template>
      </el-table-column>
      <el-table-column label="操作" width="310" align="center">
        <template slot-scope="scope">
          <span class="handle">删除</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="handle">修改</span>
        </template>
      </el-table-column>
      <el-table-column class-name="status-col" label="入库时间" width="210" align="center">
        <template slot-scope="scope">
          <i class="el-icon-time"/>
          <span>{{ scope.row.display_time }}</span>
        </template>
      </el-table-column>
    </el-table>
    
     <el-dialog
      title="温馨提示"
      :visible.sync="dialogVisible"
      width="30%"
      :before-close="handleClose">
      <span>样品编号为PL003的样品已过期请重新办理</span>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="dialogVisible = false">我知道了</el-button>
      </span>
    </el-dialog>
  </div>
  
</template>

<script>
import { getList } from '@/api/table'

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      list: null,
      listLoading: true,
      dialogVisible: false
    }
  },
  created() {
    this.fetchData()
  },
  mounted() {
    var self = this;
    setTimeout(() => {
      self.dialogVisible = true;
    }, 200)
  },
  methods: {
    fetchData() {
      // this.listLoading = true
      // getList(this.listQuery).then(response => {
      //   this.list = response.data.items
      //   this.listLoading = false
      // })
       var list = [
        {
          title: "PL001",
          address: "二楼 203",
          store: 100,
          warn: "已归还",
          display_time: "2019-03-12 22:09"
        },
        {
          title: "PL002",
          address: "五楼 504",
          store: 100,
          warn: "需归还",
          display_time: "2019-03-15 22:09"
        },
        {
          title: "PL003",
          address: "六楼 609",
          store: 100,
          warn: "已过期",
          display_time: "2019-03-16 22:09"
        },
        {
          title: "PL004",
          address: "七楼 712",
          store: 100,
          warn: "销毁中...",
          display_time: "2019-03-17 22:09"
        }
      ];
      this.listLoading = false
      this.list = list;
    },
    handleClose(done) {
      done();
        // this.$confirm('确认关闭？')
        //   .then(_ => {
        //     done();
        //   })
        //   .catch(_ => {});
      }
  }
}
</script>
<style lang="scss">
  .handle{
    color: #f45;
    cursor: pointer;
  }
  .min-img{
    width: 20px;
    float: right;
  }
</style>