
<template>
  <div class="index">
    <div class="home-wrapper">
      <div class="header">
        <div class="logo">
          <img class="left-logo" src="@/assets/img/img05.png" alt="">
          <img class="right-logo" src="@/assets/img/img01.png" alt="">
        </div>
      </div>
      <div class="content">
        <div class="main-page">
          <img src="@/assets/img/img10.jpg" alt="">
          <div class="panel">
            <div class="text">At Scamscan, we provide knowledge of onlinescams andtrain vou to protectvour data.Because scammers won't give vouconsideration for being retired</div>
            <div class="btn" @click="toDashboardFn">Protect yourself today</div>
          </div>
        </div>
        <!-- <div class="btn-group">
          <a-button type="primary" @click="toDashboardFn">Start Now</a-button>
        </div> -->
      </div>
      <div class="footer">
        <img class="left-logo" src="@/assets/img/img06.png" alt="">
      </div>
    </div>
  </div>

</template>
<script setup>
  import { useRouter } from "vue-router";
  const router = useRouter();
  const toDashboardFn = ()=>{
    router.push("/dashboard");
  }
</script>
<style scoped>
  .index{
    width:100%;
    height: 100%;
    position: relative;
  }
  .home-wrapper {
    font-size: 20px;
    line-height: 36px;
  }
  .home-wrapper .header{
    width: 100%;
    height: 94px;
    background-color: #135592;
    padding:0 30px;
  }
  .home-wrapper .header .logo{
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;

  }
  .home-wrapper .header .logo img.left-logo{
    width: 350px;
  }
  .home-wrapper .header .logo img.right-logo{
    width: 82px;
  }
  .home-wrapper .content{
    background-color: #89aac8;
    overflow: hidden;
  }
  .content .main-page{
    position: relative;
  }
  .content .main-page .panel{
    width: 600px;
    position: absolute;
    left:10%;
    top:50%;
    transform:translateY(-50%);
    font-size: 30px;
    color: #fff;
    line-height: 36px;
  }
  .content .main-page .panel .btn{
    width:380px;
    height: 72px;
    text-align: center;
    line-height: 72px;
    font-size: 30px;
    font-weight: bold;
    letter-spacing: 1px;
    background-color: #2169ab;
    border-radius: 6px;
    margin-top: 40px;
    cursor: pointer;
  }
  .content .main-page .panel .btn:hover{
    background-color: #2677c2;
  }
  .content .main-page img {
    width: 100%;
    display: block;
    height: 100%;
  }
  .home-wrapper .content .btn-group{
    margin-top: 50px;
    display: flex;
    justify-content: center;
  }
  .home-wrapper .content .btn-group button{
    background-color: #135592;
    letter-spacing: 1px;
    font-weight: bold;
    width: 250px;
    height: 60px;
    font-size: 30px;
  }
  .home-wrapper .content .btn-group button:hover{
    background-color: #1569b8;
  }
  .footer{
    height: 82px;
    width:100%;
    background-color: #d9d9d9;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding:0 20px;
  }
</style>
