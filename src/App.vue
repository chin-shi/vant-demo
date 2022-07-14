<script setup lang="ts">
import { onMounted, reactive, ref } from "vue";
import { Toast } from "vant";
import "vant/es/toast/style";

const nsrsbh = ref("");
const username = ref("");
const password = ref("");
const code = ref("");

const loading = ref(true);
const group: any = reactive([]);

onMounted(() => {
  setTimeout(() => {
    loading.value = false;
    group.push(...[1, 2, 3, 4, 5, 6]);
    console.log(group);
  }, 2000);
});

const handleHelp = () => {
  Toast.success("成功文案");
};

const onSubmit = (values: any) => {
  console.log("submit", values);
};
</script>

<template>
  <div id="app">
    <van-nav-bar title="认证">
      <template #right>
        <van-icon name="question-o" size="18" @click="handleHelp" />
      </template>
    </van-nav-bar>
    <van-notice-bar
      left-icon="volume-o"
      text="无论我们能活多久，我们能够享受的只有无法分割的此刻，此外别无其他。"
    />
    <van-divider />
    <van-notice-bar
      left-icon="volume-o"
      text="生命远不止连轴转和忙到极限，人类的体验远比这辽阔、丰富得多。"
    />
    <br />
    <van-skeleton title :row="5" :loading="loading">
      <van-form @submit="onSubmit">
        <van-cell-group inset>
          <van-field
            v-model="nsrsbh"
            name="nsrsbh"
            center
            left-icon="credit-pay"
            placeholder="统一社会信用代码"
            :rules="[{ required: true, message: '请填写统一社会信用代码' }]"
            v-if="group.includes(1)"
          />
          <van-field
            v-model="username"
            name="username"
            center
            left-icon="user-o"
            placeholder="账户"
            :rules="[{ required: true, message: '请填写账户' }]"
            v-if="group.includes(2)"
          />
          <van-field
            v-model="password"
            type="password"
            name="password"
            center
            left-icon="idcard"
            right-icon="closed-eye"
            placeholder="密码"
            :rules="[{ required: true, message: '请填写密码' }]"
            v-if="group.includes(3)"
          />
          <van-field
            v-model="code"
            name="code"
            center
            left-icon="records"
            placeholder="验证码"
            :rules="[{ required: true, message: '请填写验证码' }]"
            v-if="group.includes(5)"
          >
            <template #button>
              <van-button size="small" type="primary">发送验证码</van-button>
            </template>
          </van-field>
          <van-field
            name="other"
            center
            is-link
            readonly
            left-icon="other-pay"
            placeholder="其他认证"
            v-if="group.includes(6)"
          />
        </van-cell-group>
        <div style="margin: 16px">
          <van-button round block type="primary" native-type="submit">
            登录认证
          </van-button>
        </div>
      </van-form>
    </van-skeleton>
    <!-- 开启底部安全区适配 -->
    <van-number-keyboard safe-area-inset-bottom />
  </div>
</template>

<style>
#app {
  height: 100vh;
  background-color: #f8f8f8;
}
.vant {
  font-size: 30px;
}
</style>
