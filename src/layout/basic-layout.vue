<template>
  <a-layout class="layout my-layout">
    <a-layout-header>
      <a-menu
        v-model:selectedKeys="selectedKeys"
        theme="dark"
        mode="horizontal"
        :style="{ lineHeight: '64px' }"
        @click="handleMenuClick"
      >
        <a-menu-item key="/">Main</a-menu-item>
        <a-menu-item key="dashboard">Dashboard</a-menu-item>
        <a-menu-item key="quiz">Quiz</a-menu-item>
        <a-menu-item key="scam">Report Scam</a-menu-item>
        <a-menu-item key="scan">Scan</a-menu-item>
      </a-menu>
    </a-layout-header>
    <a-layout-content>
      <div class="content">
        <router-view></router-view>
      </div>
    </a-layout-content>
  </a-layout>
</template>
<script setup>
  import { onMounted, ref } from 'vue';
  import { useRouter, useRoute } from "vue-router";
  const router = useRouter();
  const route = useRoute();
  const selectedKeys = ref(['dashboard']);
  // 处理菜单项点击事件
  const handleMenuClick = (key) => {
    selectedKeys.value = [key];
    router.push(key.key);
  };
  onMounted(()=>{
    console.log(route);
    selectedKeys.value = [route.name];
  })
</script>
<style scoped>
  .content{
    
    height: calc(100vh - 64px);
    overflow: auto;
  }
  .ant-layout-header{
    background-color: #135592;
  }
  .ant-layout-header .ant-menu.ant-menu-overflow.ant-menu.ant-menu-root.ant-menu-horizontal.ant-menu-dark{
    background-color: #135592;
  }
  
</style>
<style>
  .my-layout .ant-layout-header .ant-menu-overflow li{
    letter-spacing: 1px;
    font-weight: bold;
  }
  .my-layout .ant-layout-header .ant-menu-overflow li.ant-menu-item-selected.ant-menu-item-only-child{
    background-color: #0f3e6a;
  }
</style>