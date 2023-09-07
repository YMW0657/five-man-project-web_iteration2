<template>
  <div class="dashboard">
    <div class="header-wrapper">
      <div class="header-title">
        What is internet fraud?
      </div>
      <div class="header-desc">
        Online fraud is everywhere: scam emails, phishing sites, text spoofing, andscams targeting seniors, Protecting information and being vigilant is crucial.
      </div>
    </div>
    <div class="dash-lists">
      <div class="dash-list">
        <div class="dash-list-title">Fraud Email</div>
        <div class="dash-list-content">
          <div class="dash-list-content-img"><img src="@/assets/img/mail.png" alt=""></div>
          <div class="dash-list-content-desc">A fraud email is a deceptivemessage designed to trickyou into revealing personaor financial information</div>
        </div>
      </div>
      <div class="dash-list">
        <div class="dash-list-title">Phishing Scam</div>
        <div class="dash-list-content">
          <div class="dash-list-content-img"><img src="@/assets/img/phishing.png" alt=""></div>
          <div class="dash-list-content-desc">A fishing website mimics alegitimate site to trick usersinto revealing personalinformation.</div>
        </div>
      </div>
    </div>
    <div class="dash-lists">
      <div class="dash-list">
        <div class="dash-list-title">SMS Scam</div>
        <div class="dash-list-content">
          <div class="dash-list-content-img"><img src="@/assets/img/smartphone.png" alt=""></div>
          <div class="dash-list-content-desc">An SMS scamis afraudulent text messagedesigned to trick recipientsinto divulging personal orfinancialinformation.</div>
        </div>
      </div>
      <div class="dash-list">
        <div class="dash-list-title">Scams Targeting Elderly</div>
        <div class="dash-list-content">
          <div class="dash-list-content-img"><img src="@/assets/img/couple.png" alt=""></div>
          <div class="dash-list-content-desc">Scams targeting the elderloften exploit their limitedunderstanding oftechnology or prey on theirtrust to extract money orpersonalinformation.</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>

</script>
<style scoped>
  .dashboard {
    width: 100%;
    height: calc(100vh - 64px);
    background-color: #efefef;
    padding:0 16%;
    overflow: auto;
  }
  .header-wrapper{
    background-color: #fff;
    padding:16px;
    margin-top: 30px;
  }
  .header-title{
    color:#000000;
    font-size: 36px;
    letter-spacing: 1px;
    font-weight: bold;
    margin-top: 14px;
    margin-bottom: 10px;
  }
  .header-desc{
    font-size: 16px;
    letter-spacing: 1px;
    font-weight: bold;
  }
  .dash-lists{
    display: flex;
    margin-top: 24px;
    justify-content: space-between;
  }
  .dash-list{
    width: 450px;
    padding:24px;
    border-radius: 8px;
    background-color: #fff;
  }
  .dash-list-title{
    font-size: 30px;
    text-align: center;
    color: #135592;
    font-weight: bold;
  }
  .dash-list-content {
    display: flex;
    justify-items: center;
    margin-top: 12px;
  }
  .dash-list-content-img img{
    width: 120px;
  }
  .dash-list-content-desc{
    font-size: 20px;
    line-height: 24px;
    padding: 12px 12px 12px 24px;
  }
</style>
