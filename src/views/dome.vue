<template>
  <div>
    <a-header class="">
      <div style="display: flex">
        <el-button type="primary" @click="vshow = !vshow">{{
          vshow ? "edtior身份" : "admin身份"
        }}</el-button>
        <template v-if="!vshow">
          <div style="width: 200px">
            <el-input v-model="input" placeholder="请输入内容"></el-input>
          </div>
          <div style="width: 200px">
            <el-select v-model="value" placeholder="请选择">
              <el-option label="身份1" value="身份1"></el-option>
              <el-option label="身份2" value="身份2"></el-option>
            </el-select>
          </div>
        </template>
      </div>
    </a-header>
    <a-main style=" padding-top: 50px;">
      <el-form ref="ruleForm" :model="form" :rules="rules" label-width="80px">
        <el-form-item label="日期" prop="date">
            <el-date-picker type="date" placeholder="选择日期" value-format="yyyy-MM-dd" v-model="form.date" style="width: 100%;"></el-date-picker>
        </el-form-item>
        <el-form-item label="姓名" prop="name">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="地址" prop="address">
          <el-input v-model="form.address"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="onSubmit('ruleForm')">立即创建</el-button>
          <el-button>取消</el-button>
        </el-form-item>
      </el-form>
    </a-main>
    <a-footer>
       <el-table :data="tableData" style="width: 100%; padding-top: 50px;">
        <el-table-column prop="date" label="日期" width="180">
        </el-table-column>
        <el-table-column prop="name" label="姓名" width="180">
        </el-table-column>
        <el-table-column prop="address" label="地址"> </el-table-column>
      </el-table>
    </a-footer>
  </div>
</template>

<script>
import AHeader from '../components/Aheader.vue'
import AMain from '../components/Amain.vue'
import AFooter from '../components/Afooter.vue'
import axios from 'axios'
export default {
  name: 'DOme',
  components: {
    AHeader,
    AMain,
    AFooter
  },
  data () {
    return {
      input: '',
      value: '',
      vshow: false,
      tableData: [],
      form: {
        name: '',
        date: '',
        address: ''
      },
      rules: {
        name: [
          { required: true, message: '请输入名称', trigger: 'blur' },
          { min: 2, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        address: [
          { required: true, message: '请输入地址', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        date: [
          { required: true, message: '请选择日期', trigger: 'change' }
        ]

      }
    }
  },
  methods: {
    init () {
      axios.get('http://localhost:8080/getUserList').then(res => {
        console.log(res.data)
        if (res.status === 200) {
          this.tableData = res.data
        }
      }).catch(err => {
        console.log(err)
      })
    },
    onSubmit (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.tableData.push(this.form)
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  },
  mounted () {
    this.init()
  }
}
</script>

<style></style>
