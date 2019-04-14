<template>
  <div class="app-container">
    <el-table
      v-loading="listLoading"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row>
      <el-table-column align="center" label="耗材编号" width="95">
        <template slot-scope="scope">
          {{ scope.row.title }}
        </template>
      </el-table-column>
      <el-table-column label="耗材位置">
        <template slot-scope="scope">
          {{ scope.row.address }} <img class="min-img" src="@/assets/pic.png"/>
        </template>
      </el-table-column>
      <el-table-column label="水位提醒" width="110" align="center">
        <template slot-scope="scope">
          <span :class="{handle: scope.row.warn != '正常'}">{{ scope.row.warn }}</span>
        </template>
      </el-table-column>
      <el-table-column label="库存" width="110" align="center">
        <template slot-scope="scope">
          {{ scope.row.store }}
        </template>
      </el-table-column>
      <el-table-column class-name="status-col" label="操作" width="300" align="center">
        <template slot-scope="scope">
          <span class="handle">删除</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="handle">修改</span>
        </template>
      </el-table-column>
      <el-table-column align="center" prop="created_at" label="有效期" width="200">
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
      //   console.log(response.data.items)
      //   this.list = response.data.items
      //   this.listLoading = false
      // })
      var list = [
        {
          title: "PL001",
          address: "二楼 203",
          store: 100,
          warn: "正常",
          display_time: "2019-03-12 22:09"
        },
        {
          title: "PL002",
          address: "二楼 204",
          store: 100,
          warn: "过高",
          display_time: "2019-03-15 22:09"
        },
        {
          title: "PL003",
          address: "二楼 209",
          store: 100,
          warn: "正常",
          display_time: "2019-03-16 22:09"
        },
        {
          title: "PL004",
          address: "二楼 212",
          store: 100,
          warn: "过低",
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