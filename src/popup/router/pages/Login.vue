<template>
  <div class="login-wrap">
    <img class="logo" src="/icons/qos.png" alt="qos logo" />
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" class="demo-ruleForm">
      <el-form-item label prop="pwd">
        <el-input v-model="ruleForm.pwd" placeholder="请输入登录密码"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button class="btn btn-login" type="primary" @click="submitLogin('ruleForm')">进入我的钱包</el-button>
      </el-form-item>
    </el-form>
    <div style="text-align:left;height:30px;">
      <el-link target="_blank" @click="forgetPassword">忘记密码？</el-link>
    </div>
    <div style="text-align:left;height:30px;">
      <el-link target="_blank" @click="noWallet">没有钱包？</el-link>
    </div>
  </div>
</template>

<script>

import {getCurrentAcount} from '../../../business/auth';
import Account from 'qosWeb/build/main/core/Account';

export default {
  data() {
    return {
      ruleForm: {
        pwd: '',
        defaultAccount:  {}
      },
      rules: {
        pwd: [
          { required: true, message: "请输入登录密码", trigger: "blur" },
          { min: 6, max: 30, message: "长度在 6 到 30 个字符", trigger: "blur" }
        ]
      }
    };
  },
  methods: {
    forgetPassword() {
      this.$router.push("/importwalletwithseed");
    },
    noWallet() {
      this.$router.push("/newwallet");
    }
  },
  submitLogin () {
    if (!isNotEmpty(this.data.pwd)) {
        console.log('pwd is empty');
        return
      }
    var password = this.data.pwd;
      const currentAccount = getCurrentAcount();
      console.log(currentAccount);
      if (currentAccount)  { 
        accountList.forEach(acc => {
          if (Account(acc).name ===accountName){
            console.log('dup account name');
            return 
          }
          console.log(acc)
        }); 

    console.log('login')
  }
}
}
</script>

<style lang="scss" scoped>
.login-wrap {
  width: 308px;
  padding: 30px 20px;
  .logo {
    width: 20%;
    display: block;
    margin: 0 auto;
    margin-bottom: 20px;
  }
  .btn-login {
    width: 100%;
  }
}
</style>
