<script setup lang="ts">
import {ref, computed} from 'vue'
// 输入框值（需要在前端拦截不合法输入：是否为空+额外规则）
const name = ref('')
const identity = ref('')
const address = ref('')
const password = ref('')
const confirmPassword = ref('')
// 密码是否为空
const hasPasswordInput = computed(() => password.value != '')
// 重复密码是否为空
const hasConfirmPasswordInput = computed(() => confirmPassword.value != '')
// 地址是否为空
const hasAddressInput = computed(() => address.value != '')
// 身份是否为空
const hasIdentityChosen = computed(() => identity.value != '')
// 重复密码的规则
const isPasswordIdentical = computed(() => password.value == confirmPassword.value)
// 注册按钮可用性
const registerDisabled = computed(() => {
  if (hasPasswordInput.value && hasConfirmPasswordInput && hasAddressInput.value && isPasswordIdentical.value) {
    return true
  }
})

// 注册按钮触发
function handleRegister() {

}
</script>


<template>
  <div class="background">
  <el-main class="main-frame bgimage">
    <el-card class="login-card">
      <div>
        <h2>创建新用户</h2>

        <el-form>
          <el-row>
              <el-form-item>
                <label for="name">用户名</label>
                <el-input id="name"
                          v-model="name"
                          placeholder="请输入用户名"/>
              </el-form-item>
          </el-row>



        <el-row>
          <el-form-item>
            <label for="password">密码</label>
            <el-input type="password" id="password"
                      v-model="password"
                      placeholder="••••••••"/>
            <el-col :span="8">
            </el-col>
          </el-form-item>
        </el-row>
          <el-form-item>
            <label v-if="!hasConfirmPasswordInput">确认密码</label>
            <label v-else-if="!isPasswordIdentical" class="error-warn">密码不一致</label>
            <label v-else>确认密码</label>

            <el-input type="password" id="confirm-password"
                      v-model="confirmPassword"
                      :class="{'error-warn-input' :(hasConfirmPasswordInput && !isPasswordIdentical)}"
                      placeholder="••••••••"/>
          </el-form-item>

          <span class="button-group">
            <el-button @click.prevent="handleRegister"
                       :disabled="registerDisabled"
                       type="primary">
              创建用户
            </el-button>

            <router-link to="/login" v-slot="{navigate}">
              <el-button @click="navigate">
                去登录
              </el-button>
            </router-link>
          </span>

        </el-form>
      </div>

    </el-card>
  </el-main>
  </div>
</template>


<style scoped>
.main-frame {
  width: 100%;
  height: 100%;

  display: flex;
  align-items: center;
  justify-content: center;
}

.login-card {
  width: 60%;
  padding: 10px;
}

.error-warn {
  color: red;
}

.error-warn-input {
  --el-input-focus-border-color: red;
}

.button-group {
  padding-top: 10px;
  display: flex;
  flex-direction: row;
  gap: 30px;
  align-items: center;
  justify-content: right;
}

.background{
  background: -webkit-linear-gradient(left,#85C1E9,#6C3483) no-repeat;
}

</style>
