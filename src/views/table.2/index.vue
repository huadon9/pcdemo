<template>
  <div class="app-container">
    <el-table
      v-loading="listLoading"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row>
      <el-table-column align="center" label="仪器编号" width="95">
        <template slot-scope="scope">
          {{ scope.row.title }}
        </template>
      </el-table-column>
      <el-table-column label="仪器名称" width="200">
        <template slot-scope="scope">
          {{ scope.row.name }}
        </template>
      </el-table-column>
      <el-table-column label="仪器位置"  align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.address }}</span><img class="min-img" src="@/assets/pic.png"/>
        </template>
      </el-table-column>
      <el-table-column label="仪器状态" width="110" align="center">
        <template slot-scope="scope">
          <span :class="{handle: scope.row.warn != '正常'}">{{ scope.row.warn }}</span>
        </template>
      </el-table-column>
      <el-table-column class-name="status-col" label="额定参数" width="110" align="center">
        <template slot-scope="scope">
          {{ scope.row.store }}
        </template>
      </el-table-column>
       <el-table-column class-name="status-col" label="操作" width="210" align="center">
        <template slot-scope="scope">
          <span class="handle">删除</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="handle">修改</span>
        </template>
      </el-table-column>
      <el-table-column align="center" prop="created_at" label="校准时间" width="200">
        <template slot-scope="scope">
          <i class="el-icon-time"/>
          <span>{{ scope.row.display_time }}</span>
        </template>
      </el-table-column>
    </el-table>
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
      listLoading: true
    }
  },
  created() {
    this.fetchData()
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
          name: "氢气发生器",
          address: "二楼 203",
          store: 100,
          warn: "正常",
          display_time: "2019-03-12 22:09"
        },
        {
          title: "PL002",
          name: "氧气发生器",
          address: "二楼 204",
          store: 100,
          warn: "维修中...",
          display_time: "2019-03-15 22:09"
        },
        {
          title: "PL003",
          name: "氧气发生器",
          address: "二楼 209",
          store: 100,
          warn: "需检修",
          display_time: "2019-03-16 22:09"
        },
        {
          title: "PL004",
          name: "氧气发生器",
          address: "二楼 212",
          store: 100,
          warn: "正常",
          display_time: "2019-03-17 22:09"
        }
      ];
      this.listLoading = false
      this.list = list;
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
