<template>
  <nav class="nav-container">
    <ul aria-label="主导航菜单">
      <li @mouseenter="hoverIndex = 0" @mouseleave="hoverIndex = null">
        <router-link to="/" exact-active-class="active">流麻成品展示</router-link>
      </li>
      <li @mouseenter="hoverIndex = 1" @mouseleave="hoverIndex = null">
        <router-link to="/uploadview" exact-active-class="active">AI绘图展示</router-link>
      </li>
    </ul>

    <!-- 头像链接 -->
    <el-tooltip class="box-item" effect="light" content="点这里跳转我的b站个人空间哦！" placement="left-start">
      <div class="avatar">
        <a href="https://space.bilibili.com/372611876?spm_id_from=333.1007.0.0" target="_blank" rel="noopener noreferrer">
          <img src="@/assets/avatar.jpeg" alt="B站账号头像" />
        </a>
      </div>
    </el-tooltip>
  </nav>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const activeIndex = computed(() => {
  if (route.path === '/') return 0;
  if (route.path === '/uploadview') return 1;
  return 0;
});

const hoverIndex = ref(null);
</script>

<style scoped lang="scss">
$primary-color: rgb(70, 100, 180);

* {
  margin: 0;
  padding: 0;
  list-style: none;
}

.nav-container {
  width: 100%;
  position: relative;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.5);
  background-color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px;  /* 增加左右内边距，避免内容贴边 */
  height: 70px;
  .logo {
    font-size: clamp(24px, 5vw, 32px);
    font-style: italic;
    cursor: pointer;
    color: inherit;
  }

  ul {
    display: flex;
    align-items: center;
    justify-content: space-around;
    width: 100%;
    height: 100%;
    position: relative;
    padding: 0;
    margin-top: 10px;
    flex-direction: row;
  }

  li {
    flex: 1;
    text-align: center;

    a {
      color: $primary-color;
      font-weight: 100;
      font-size: 18px;
      text-decoration: none;
      display: block;
      line-height: 3rem;
    }

    /* 路由激活状态样式 */
    a.active {
      font-weight: bold;
    }
  }

  .avatar {
    height: 50px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 10px;

    img {
      width: 40px;
      height: 40px;
      border-radius: 50%;
    }
  }
}


</style>
