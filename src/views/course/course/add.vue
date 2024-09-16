<template>
  <div>
    <el-form ref="elForm" :model="formData" :rules="rules" size="medium" label-width="100px">
      <el-row gutter="15">
        <el-col :span="10">
          <el-form-item label="课程编号" prop="code">
            <el-input v-model="formData.code" placeholder="请输入课程编号" clearable :style="{width: '100%'}">
            </el-input>
          </el-form-item>
        </el-col>
        <el-col :span="10">
          <el-form-item label="课程学科" prop="subject">
            <el-select v-model="formData.subject" placeholder="请选择课程学科" clearable :style="{width: '100%'}">
              <el-option v-for="(item, index) in subjectOptions" :key="index" :label="item.label"
                :value="item.value" :disabled="item.disabled"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="10">
          <el-form-item label="课程名称" prop="field105">
            <el-input v-model="formData.field105" placeholder="请输入课程名称" clearable :style="{width: '100%'}">
            </el-input>
          </el-form-item>
        </el-col>
        <el-col :span="10">
          <el-form-item label="课程价格" prop="field106">
            <el-input v-model="formData.field106" placeholder="请输入课程价格" clearable :style="{width: '100%'}">
            </el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="10">
          <el-form-item label="适用人群" prop="field108">
            <el-select v-model="formData.field108" placeholder="请选择适用人群" clearable :style="{width: '100%'}">
              <el-option v-for="(item, index) in field108Options" :key="index" :label="item.label"
                :value="item.value" :disabled="item.disabled"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="10">
          <el-form-item label="课程有效期" prop="field109">
            <el-date-picker type="daterange" v-model="formData.field109" format="yyyy-MM-dd"
              value-format="yyyy-MM-dd" :style="{width: '100%'}" start-placeholder="开始日期"
              end-placeholder="结束日期" range-separator="至" clearable></el-date-picker>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="10">
          <el-form-item label="课程封面" prop="field111" required>
            <el-upload ref="field111" :file-list="field111fileList" :action="field111Action"
              :before-upload="field111BeforeUpload">
              <el-button size="small" type="primary" icon="el-icon-upload">点击上传</el-button>
            </el-upload>
          </el-form-item>
        </el-col>
        <el-col :span="10">
          <el-form-item label="推荐指数" prop="field112">
            <el-rate v-model="formData.field112"></el-rate>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="18">
          <el-form-item label="课程介绍" prop="field115">
            <el-input v-model="formData.field115" type="textarea" placeholder="请输入课程介绍"
              :autosize="{minRows: 4, maxRows: 4}" :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-form-item size="large">
        <el-button type="primary" @click="submitForm">提交</el-button>
        <el-button @click="resetForm">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  components: {},
  props: [],
  data() {
    return {
      formData: {
        code: undefined,
        subject: undefined,
        field105: undefined,
        field106: undefined,
        field108: undefined,
        field109: null,
        field111: null,
        field112: 0,
        field115: undefined,
      },
      rules: {
        code: [{
          required: true,
          message: '请输入课程编号',
          trigger: 'blur'
        }],
        subject: [{
          required: true,
          message: '请选择课程学科',
          trigger: 'change'
        }],
        field105: [{
          required: true,
          message: '请输入课程名称',
          trigger: 'blur'
        }],
        field106: [{
          required: true,
          message: '请输入课程价格',
          trigger: 'blur'
        }],
        field108: [{
          required: true,
          message: '请选择适用人群',
          trigger: 'change'
        }],
        field109: [{
          required: true,
          message: '课程有效期不能为空',
          trigger: 'change'
        }],
        field112: [{
          required: true,
          message: '推荐指数不能为空',
          trigger: 'change'
        }],
        field115: [{
          required: true,
          message: '请输入课程介绍',
          trigger: 'blur'
        }],
      },
      field111Action: 'https://jsonplaceholder.typicode.com/posts/',
      field111fileList: [],
      subjectOptions: [{
        "label": "选项一",
        "value": 1
      }, {
        "label": "选项二",
        "value": 2
      }],
      field108Options: [{
        "label": "选项一",
        "value": 1
      }, {
        "label": "选项二",
        "value": 2
      }],
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  methods: {
    submitForm() {
      this.$refs['elForm'].validate(valid => {
        if (!valid) return
        // TODO 提交表单
      })
    },
    resetForm() {
      this.$refs['elForm'].resetFields()
    },
    field111BeforeUpload(file) {
      let isRightSize = file.size / 1024 / 1024 < 2
      if (!isRightSize) {
        this.$message.error('文件大小超过 2MB')
      }
      return isRightSize
    },
  }
}

</script>
<style>
.el-upload__tip {
  line-height: 1.2;
}

.el-rate {
  display: inline-block;
  vertical-align: text-top;
}

</style>
