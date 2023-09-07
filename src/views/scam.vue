<template>
  <div class="scam">
    <div class="scam-wrapper">
      <div class="scam-header">
        Fall victim to a scam? Report it to
      </div>
      <div class="scam-lists">
        <div class="scam-list" v-for="item in items" :key="item.org_name">
          <div class="scam-list-left">
            <img :src="item.logo" alt="">
          </div>
          <div class="scam-list-right">
            <div class="scam-list-right-title">{{ item.org_name }}</div>
            <div class="scam-list-right-desc">{{ item.description }}</div>
            <div class="scam-list-right-btns">
              <span><a :href="item.link">Go To Website</a></span>
            </div>
          </div>
        </div>
      </div> 
    </div>
  </div>
</template>
<script setup>
  import {ref} from "vue";
  const items = ref([
    {
        "logo" : "src/assets/img/OAIC.png",
        "org_name" : "OAIC",
        "description" : "The Office of the Australian Information Commissioner (OAIC) oversees data protection, privacy, and access to government information. It ensures compliance, promotes transparency, and safeguards personal and public data.",
        "link" : "https://www.oaic.gov.au/"
    },
    {
        "logo" : "src/assets/img/Scamwatch.png",
        "org_name" : "Scamwatch",
        "description" : "Scamwatch is an Australian government initiative that empowers individuals and businesses to recognize, report, and stay informed about scams, fostering a safer digital environment through awareness and prevention.",
        "link" : "https://www.scamwatch.gov.au/report-a-scam"
    },
    {
        "logo": "src/assets/img/ACSC.png",
        "org_name" : "ACSC",
        "description" : "The Australian Cyber Security Centre (ACSC) is a government agency that safeguards Australia's digital landscape. It provides cybersecurity guidance, threat intelligence, and collaboration to defend against online threats and attacks.",
        "link" : "https://www.cyber.gov.au/report-and-recover/report"
    }
  ])
</script>
<style scoped>
  .scam{
    width:100%;
    height: calc(100vh - 64px);
    overflow: auto;
  }
  .scam-wrapper{
    padding:20px 16%;
  }
  .scam-header{
    color: #135592;
    font-weight: bold;
    font-size: 60px;
    letter-spacing: 1px;
    text-align: center;
  }
  .scam-lists{
    margin-top: 60px;
  }
  .scam-list{
    display: flex;
    border:1px solid #ddd;
    align-items: center;
    background-color: #f8f7f2;
    padding:12px;
    width: 90%;
    margin: 40px auto 0;
  }
  .scam-list-left{
    width: 300px;
    display:flex;
    justify-content: center;
    align-items: center;
    padding: 30px 0;
  }
  .scam-list-left img{
    width:200px;
  }
  .scam-list-right{
    width: calc(100vw - 700px);
    padding-left: 30px;
  }
  .scam-list-right-title{
    color: #135592;
    font-size:30px;
    font-weight: bold;
  }
  .scam-list-right-desc{
  color: #000;
    line-height: 24px;
    font-size: 16px;
    margin: 12px 0 24px 0;
    font-weight: bold;
  }
  .scam-list-right-btns{

  }
  .scam-list-right-btns span a{
    padding:4px 20px;
    background-color: #135592;
    text-align: center;
    color: #fff;
    border-radius: 13px ;
    cursor: pointer;
  }
  .scam-list-right-btns span a:hover{
    background-color: #206fba;
  }
</style>