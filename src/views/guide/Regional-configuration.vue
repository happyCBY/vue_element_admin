<template>
  <div class="app-container">
    <div class="filter-container">
      <el-button style="vertical-align: top;" @click="add">添加</el-button>
      <el-input v-model="listQuery.UserMobile" placeholder="手机号/用户名" style="width: 200px;" class="filter-item mgL " />
      <el-dropdown class="mgL">
        <el-button>
          区域筛选<i class="el-icon-arrow-down el-icon--right" />
        </el-button>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>浙江省</el-dropdown-item>
          <el-dropdown-item>浙江省</el-dropdown-item>
          <el-dropdown-item>浙江省</el-dropdown-item>
          <el-dropdown-item>浙江省</el-dropdown-item>
          <el-dropdown-item>浙江省</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>

      <el-table
        v-loading="listLoading"
        :data="list"
        border
        fit
        highlight-current-row
        style="width: 100%;"
      >
        <el-table-column label="序号ID" prop="id" align="center" width="65">
          <template slot-scope="scope">
            <span>{{ scope.row.Userid }}</span>
          </template>
        </el-table-column>
        <el-table-column label="账号" width="110px" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.Mobile }}</span>
          <!--scope.row.timestamp | parseTime('{y}-{m}-{d} {h}:{i}')-->
          </template>
        </el-table-column>
        <el-table-column label="用户手机号" width="110px" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.Phone }}</span>
          </template>
        </el-table-column>
        <el-table-column label="推荐人" width="110px" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.recommender }}</span>
          </template>
        </el-table-column>
        <el-table-column label="代理区域" width="160px" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.dlqy }}</span>
          </template>
        </el-table-column>
        <el-table-column label="区域业绩" width="160px" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.qyyj }}</span>
          </template>
        </el-table-column>
        <el-table-column label="时间" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.time }}</span>
          </template>
        </el-table-column>
        <el-table-column label="操作" align="center">
          <template slot-scope="scope">
            <span><a href="javascript:;" @click="updateQy(scope.row.Userid)">修改</a></span>
            <span><a href="javascript:;" @click="details(scope.row.Userid)">详情</a></span>
            <span><a href="javascript:;" style="color: red" @click="deleteQy(scope.row.Userid)">删除</a></span>
          </template>
        </el-table-column>
      </el-table>
      <p style="text-align: right">
        <pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getRegionalList" />
      </p>
    </div>
  </div>
</template>
<script>
import { getList } from '@/api/user'
import Pagination from '@/components/Pagination'
export default {
  components: { Pagination },
  data() {
    return {
      listLoading: true,
      list: [],
      listQuery: {
        page: 1,
        limit: 10,
        FavorKey: '',
        UserMobile: '',
        date: ''
      },
      total: 0
    }
  },
  created() {
    this.getRegionalList()
  },
  methods: {
    // 添加
    add() {
      this.$router.push('/guide/AddQyPeo')
    },
    // 获得列表
    getRegionalList() {
      getList().then(response => {
        this.list = response.data
        this.total = response.data.length
      })
      this.listLoading = false
    },
    // 修改区域配置
    updateQy() {
      this.$router.push('/guide/updataMsg')
    },
    // 删除
    deleteQy(id) {

    }
  }
}
</script>
<style  scoped>
a {
  margin-right: 10px;
}
</style>
