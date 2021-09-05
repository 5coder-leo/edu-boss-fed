<template>
  <div class="login">
    <el-form
      ref="form"
      :model="form"
      :rules="rules"
      label-position="top"
      label-width="80px"
      class="login-form"
    >
      <h3>登录</h3>
      <el-form-item label="手机号" prop="phone">
        <el-input v-model="form.phone"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input type="password" v-model="form.password"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button
          type="primary"
          class="login-btn"
          @click="onSubmit"
          :loading="isLoginLoading"
        >登录
        </el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Form } from 'element-ui'
import request from '@/utils/request'
import qs from 'qs'
import { login } from '@/services/user'

export default Vue.extend({
  name: 'LoginIndex',
  data () {
    return {
      form: {
        phone: '18201288771',
        password: '111111'
      },
      rules: {
        phone: [
          {
            required: true,
            message: '请输入手机号',
            trigger: 'blur'
          },
          {
            pattern: /^1\d{10}$/,
            message: '请输入正确的手机号'
          }
        ],
        password: [
          {
            required: true,
            message: '请输入密码',
            trigger: 'blur'
          },
          {
            min: 6,
            max: 18,
            message: '长度在 6 到 18 个字符'
          }
        ]
      },
      isLoginLoading: false
    }
  },
  methods: {
    async onSubmit () {
      try {
        // 1.表单验证
        await (this.$refs.form as Form).validate()
        // 登录按钮Loading状态
        this.isLoginLoading = true
        // 2.验证通过 -《 提交表单
        const { data } = await login(this.form)
        // const { data } = await request({
        //   method: 'POST',
        //   url: '/front/user/login',
        //   headers: { 'content-type': 'application/x-www-form-urlencoded' },
        //   data: qs.stringify(this.form)
        // })
        // 3.处理请求结果
        //  失败
        if (data.state !== 1) {
          this.$message.error(data.message)
        } else {
          //  成功
          this.$router.push({
            name: 'home'
          })
          this.$message.success('登陆成功')
        }
      } catch (e) {
        console.log('登录失败', e)
      }
      // 结束登录按钮的 loading
      this.isLoginLoading = false
    }
  }
})
</script>

<style lang="scss" scoped>
.login {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;

  .login-form {
    width: 300px;
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
  }

  .login-btn {
    width: 100%;
  }
}
</style>
