<template>
  <div class="home">
    <div class="bg"></div>
    <UserInfo v-show="isShowUserInfo" @after-submit="showUserInfo(false)" />
    <header>
      <div class="icon">
        <div class="study"></div>
        <div class="school"></div>
        <div class="redrock"></div>
      </div>
      <div class="user" @click="showUserInfo(true)"></div>
    </header>
    <main>
      <div class="title"></div>
      <div class="start" @click="toSelect"></div>
    </main>
    <footer>
      <p class="ref">重庆市学生联合会、重庆邮电大学联合出品</p>
      <p class="ref">@红岩网校工作站出品</p>
    </footer>
  </div>
</template>

<script>
import UserInfo from "@components/UserInfo";
import { ref } from "vue";
import { useRouter } from "vue-router";
import { getUserInfo } from "@/services/api";
export default {
  components: { UserInfo },
  setup() {
    const isShowUserInfo = ref(false);
    const router = useRouter();
    const showUserInfo = status => {
      isShowUserInfo.value = status;
    };
    const fetchUserInfo = async () => {
      const { data } = await getUserInfo();
      if (!data.name) isShowUserInfo.value = true;
    };

    const toSelect = () => {
      router.push("/block");
    };
    fetchUserInfo();
    return {
      isShowUserInfo,
      showUserInfo,
      toSelect
    };
  }
};
</script>

<style lang="scss" socped>
.home {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
  .bg {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: -1;
    background-image: url(~@assets/images/home/bg.png);
    background-size: cover;
    background-repeat: no-repeat;
  }
  header {
    margin: 35px 35px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .icon {
      display: flex;
      .school,
      .study,
      .redrock {
        width: 66px;
        height: 66px;
        background-size: contain;
        background-repeat: no-repeat;
        margin-right: 22px;
      }
      .school {
        background-image: url(~@assets/images/home/icon_school.png);
      }
      .study {
        background-image: url(~@assets/images/home/icon_study.png);
      }
      .redrock {
        background-image: url(~@assets/images/home/icon_redrock.png);
      }
    }
    .user {
      width: 56px;
      height: 59px;
      background-image: url(~@assets/images/home/user.png);
      background-size: contain;
      background-repeat: no-repeat;
    }
  }
  main {
    width: 100%;
    .title {
      margin: 21px auto 271px;
      width: 672px;
      height: 201px;
      background-image: url(~@assets/images/home/title.png);
      background-size: contain;
      background-repeat: no-repeat;
    }
    .start {
      margin: 0 auto;
      width: 315px;
      height: 137px;
      background-image: url(~@assets/images/home/start_button.png);
      background-size: contain;
      background-repeat: no-repeat;
    }
  }
  footer {
    width: 100%;
    margin: auto 0 0;
    text-align: center;
    font-size: 24px;
    color: #ffb5a9;
    font-weight: 500;
    .ref {
      margin-bottom: 16px;
    }
  }
}
</style>
