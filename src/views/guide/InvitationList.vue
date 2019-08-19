<template>
  <div class="app-container">
    <div class="filter-container">
      <el-input v-model="listQuery.UserMobile" placeholder="手机号/用户名" style="width: 200px;" class="filter-item " />
      <el-input v-model="listQuery.FavorKey" placeholder="推荐人账号" style="width: 200px;" class="filter-item mgL" />
      <el-date-picker
        v-model="listQuery.date"
        type="daterange"
        value-format="yyyy-MM-dd"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
        class="mgL"
      />
      <el-button type="primary" icon="el-icon-search" class="mgL" @click="search">搜索</el-button>
      <el-button :loading="downloadLoading" class="mgL" style="margin:0 0 20px 20px;" type="primary" icon="document" @click="handleDownload">
        Export Excel
      </el-button>
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
        <el-table-column label="注册时间" width="160px" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.registrationTime }}</span>
          </template>
        </el-table-column>
        <el-table-column label="累计推荐人数" width="160px" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.recommenderAll }}</span>
          </template>
        </el-table-column>
        <el-table-column label="间接推荐人数" align="center">
          <template slot-scope="scope">
            <span>{{ scope.row.recommenderIndirect }}</span>
          </template>
        </el-table-column>
        <el-table-column label="操作" align="center">
          <template slot-scope="scope">
            <span><a href="javascript:;" @click="details(scope.row.Userid)">详情</a></span>
          </template>
        </el-table-column>
      </el-table>
      <p style="text-align: right">
        <pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getlist" />
      </p>
    </div>
  </div>
</template>
<script>
import { getList } from '@/api/user'
import Pagination from '@/components/Pagination'
import { parseTime } from '@/utils'
export default {
  name: 'InvitationList',
  components: { Pagination },
  data() {
    return {
      total: 0,
      list: [],
      listLoading: true,
      downloadLoading: false,
      listQuery: {
        page: 1,
        limit: 10,
        FavorKey: '',
        UserMobile: '',
        date: ''
      },
      // 导出表格名
      filename: 'cby',
      // 表格单元格是否自适应
      autoWidth: true,
      bookType: 'xlsx'
    }
  },
  created() {
    this.getlist()
  },
  methods: {
    // 获得列表
    getlist() {
      getList().then(response => {
        this.list = response.data
        this.total = response.data.length
      })

      this.listLoading = false
    },
    // 搜索
    search() {
      console.log(this.listQuery)
    },
    // 导出
    handleDownload() {
      this.downloadLoading = true
      import('@/vendor/Export2Excel').then(excel => {
        const tHeader = ['Userid', 'Mobile', 'Phone', 'recommender', 'registrationTime', 'recommenderAll', 'recommenderIndirect']
        const filterVal = ['Userid', 'Mobile', 'Phone', 'recommender', 'registrationTime', 'recommenderAll', 'recommenderIndirect']
        const list = this.list
        const data = this.formatJson(filterVal, list)
        excel.export_json_to_excel({
          header: tHeader,
          data,
          filename: this.filename,
          autoWidth: this.autoWidth,
          bookType: this.bookType
        })
        this.downloadLoading = false
      })
    },
    // 如果是时间则处理时间格式
    formatJson(filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => {
        if (j === 'timestamp') {
          return parseTime(v[j])
        } else {
          return v[j]
        }
      }))
    },
    // 点击详情
    details(id) {
      this.$router.push('/guide/details/' + id)
    }
  }
}
</script>
<style  scoped>

.app-container {
  padding: 20px;
}

</style>
