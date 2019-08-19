<template>
  <div class="app-container">
    <div class="filter-container">
      <el-row>
        <el-col :span="6">
          <span>用户名:</span>
          <el-input placeholder="请输入" class="width200" />
        </el-col>
        <el-col :span="2">&nbsp;</el-col>
        <el-col :span="6">
          <span>推荐人:</span>
          <el-input placeholder="请输入" class="width200" />
        </el-col>
      </el-row>

      <el-row class="mgT20">
        <el-col>
          <span>用户手机号:</span>
          <el-input placeholder="请输入" class="width200" />
        </el-col>
      </el-row>

      <el-row class="mgT20">
        <el-col :span="8">
          <span>代理区域</span>
          <el-dropdown @command="handleCommand">
            <el-button class="width200" style=" text-align: left ">
              <span>{{ choose }}</span><i style="float: right" class="el-icon-arrow-down el-icon--right" />
            </el-button>
            <el-dropdown-menu slot="dropdown" class="width200">
              <el-dropdown-item command="省">省</el-dropdown-item>
              <el-dropdown-item command="市">市</el-dropdown-item>
              <el-dropdown-item command="区">区</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-col>

        <el-col :span="8" style="line-height: 36px">
          <span style=" width: 200px; color: red; ">当前代理区域:{{ '西湖区' }}</span>
        </el-col>
      </el-row>

      <el-row class="mgT20">
        <el-col>
          <el-button type="primary">
            <span>保存</span>
          </el-button>
          <el-button style="border: none">
            <span>取消</span>
          </el-button>
        </el-col>
      </el-row>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      choose: '选择区域'
    }
  },
  methods: {
    // 点击菜单后触发
    handleCommand(command) {
      this.choose = command
    }
  }
}
</script>
<style  scoped>
.width200 {
    width: 180px;
}
span {
    display: inline-block;
    width: 70px;
    font-size: 12px;
    margin-right: 10px;
}

</style>
