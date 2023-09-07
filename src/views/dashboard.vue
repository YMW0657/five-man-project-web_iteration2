<template>
  <div class="dashboard">
    <div class="main-wrapper">
      <div class="main-wrapper-slide">
        <img src="@/assets/img/img08.jpg" alt="">
        <div class="main-wrapper-page">
          <div class="title">What are internet frauds?</div>
          <div class="artical">Online fraud is everywhere: scam emails, phishing sites, text spoofing, andscams targeting seniors, Protecting information and being vigilant is crucial.</div>
        </div>
      </div>
    </div>
    <div class="dashboard-lists">
      <div class="dashboard-title">
        These are the techniques to look out for
      </div>
      <div class="dashboard-list">
        <div class="dashboard-list-wrapper">
          <img src="@/assets/img/fishing.png" alt="">
          <div class="dashboard-list-wrapper-text">Phishing</div>
        </div>
        <div class="dashboard-list-wrapper">
          <img src="@/assets/img/spoofing.png" alt="">
          <div class="dashboard-list-wrapper-text">Spoofing</div>
        </div>
        <div class="dashboard-list-wrapper">
          <img src="@/assets/img/card_theft.png" alt="">
          <div class="dashboard-list-wrapper-text">Card theft</div>
        </div>
      </div>
    </div>
    <div class="dashboard-info">
      <div class="dashboard-info-left">
        <img src="@/assets/img/img06.jpg" alt="">
      </div>
      <div class="dashboard-info-right">
        <div class="dashboard-info-right-text">
          Finished reading through thosetechniques? Scamscan provide our userwith quiz for you to self-assess yourinformation security awareness levelHow about taking our quiz to checkyour readiness?
        </div>
        <div class="dashboard-info-right-btn">
          <div class="btn" @click="toQuestionFn">Start now</div>
        </div>
      </div>
    </div>

  </div>
</template>
<script setup>
  import { useRouter } from "vue-router";
  const router = useRouter();
  const toQuestionFn = ()=>{
    router.push("/quiz");
  }
</script>
<style scoped>
.dashboard{
  width:100%;
  min-height: calc(100vh - 64px);
}
.main-wrapper{
  width:100%;
}
.main-wrapper-slide{
  width:100%;
  height: 700px;
  overflow: hidden;
  position: relative;
}
.main-wrapper-slide img{
  width:100%;
}
.main-wrapper-slide .text{

}
.main-wrapper-page{
  position: absolute;
  left:10%;
  bottom:50px;
  width:80%;
  background-color: rgba(198, 198, 198, 0.5);
  border-radius: 8px;
  padding:20px;
  color: #fff;
}
.main-wrapper-page .title{
  margin-bottom: 30px;
  font-weight: bold;
  font-size: 30px;
}
.main-wrapper-page .artical{
  font-size: 20px;
}
.dashboard-lists{
  padding-top: 60px;
}
.dashboard-list{
  display:flex;
  padding:0 40px;
}
.dashboard-title{
  font-size: 30px;
  padding-left: 40px;
  color: #333;
  letter-spacing: 1px;
  margin-bottom: 24px;
}
.dashboard-list .dashboard-list-wrapper{
  width:30%;
  position: relative;
  border-radius: 12px;
  overflow: hidden;
}
.dashboard-list .dashboard-list-wrapper:nth-last-of-type(2){
  margin:0 10%;
}
.dashboard-list .dashboard-list-wrapper img{
  width:100%;
}
.dashboard-list .dashboard-list-wrapper .dashboard-list-wrapper-text{
  position: absolute;
  bottom:12px;
  left:24px;
  font-size: 18px;
  color: #fff;
  letter-spacing: 1px;
}
.dashboard-info{
  width: 100%;
  display: flex;
  padding:0 40px;
  margin-top: 60px;
}
.dashboard-info .dashboard-info-left{
  width: 60%;
}
.dashboard-info .dashboard-info-left img{
  width: 100%;
}
.dashboard-info-right{
  width: 40%;
  padding-top: 10%;
  background-color: #d9d9d9;
}
.dashboard-info-right-text{
  padding:0 40px;
  font-size: 20px;
  line-height: 32px;
}
.dashboard-info-right-btn{
  width: 100%;
  margin-top: 40px;
}
.dashboard-info-right-btn .btn{
  width:170px;
  height: 36px;
  text-align: center;
  line-height: 36px;
  color: #fff;
  font-size: 20px;
  letter-spacing: 1px;
  background-color: #608fbb;
  border-radius: 8px;
  margin:0 auto;
  cursor: pointer;
}
.dashboard-info-right-btn .btn:hover{
  background-color:#69a2d7;
}
</style>