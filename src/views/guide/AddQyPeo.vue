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
        <el-col>
          <span>代理区域:</span>
          <el-select v-model="value" placeholder="请选择" @change="handleCommand">
            <el-option
              v-for="item in options"
              :key="item.id"
              :label="item.label"
              :value="item.value"
            />
          </el-select>
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
      options: [
        {
          id: 1,
          value: '浙江省',
          label: '浙江省'
        },
        {
          id: 2,
          value: '浙江省',
          label: '浙江省'
        },
        {
          id: 3,
          value: '浙江省',
          label: '浙江省'
        }
      ],
      value: '请选择区域'
    }
  },
  methods: {
    // 选择器值发生变化时触发
    handleCommand(text) {
      console.log(text)
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
  /* text-align: right; */
}
</style>
