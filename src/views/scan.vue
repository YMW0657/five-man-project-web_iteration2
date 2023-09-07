<template>
  <div class="scan">
    <div class="scan-wrapper">
      <div class="textarea-box">
        <a-textarea
          v-model:value="question"
          class="textarea"
          placeholder="Enter your input here......"
          :auto-size="{ minRows: 8, maxRows: 8 }"
        />
      </div>
      <div class="btn-group">
        <div class="btn">Submit</div>
      </div>
      <div class="scan-result">
        <div class="left">
          <div class="progress">
            <div class="progress-wrapper" style="height:80%">
              <div class="value">80%</div>
            </div>
          </div>
        </div>
        <div class="right">
          <div class="result-deail">
            Oh oh... might be a scam
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Molestiae modi ratione rem praesentium. Ratione laborum dolorum consequatur iure dicta nisi adipisci explicabo non, aliquid ex eaque, atque cumque rem voluptas?
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
  import {ref} from "vue";
  const question = ref("");
</script>
<style scoped>
  .scan{
    height: calc(100vh - 64px);
    background-color: #fff;
  }
  .scan-wrapper{
    padding:30px;
  }
  .textarea{
    padding:12px;
    background-color: #efefef;
  }
  .btn-group{
    width:100%;
    margin:50px 0;
  }
  .btn-group .btn{
    width: 200px;
    height: 50px;
    text-align: center;
    line-height: 50px;
    background-color: #135592;
    font-size:26px;
    font-weight: bold;
    margin:0 auto;
    color: #fff;
    border-radius: 25px;
    cursor: pointer;
  }
  .btn-group .btn:hover{
    background-color: #1862a7;
  }
  .scan-result{
    display: flex;
    height: 230px;
  }
  .progress{
    height: 230px;
    width: 148px;
    background-color: #d9d9d9;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
  }
  .progress-wrapper{
    height: 0%;
    background-color: #ef3c15;
    text-align: center;
    color: #fff;
  }
  .right{
    padding-left: 40px;
  }
  .right .result-deail{
    font-size: 24px;
    line-height: 32px;
    background-color: #efefef;
    width: calc(100vw - 280px);
    height: calc(100vh - 478px);
    padding:24px;
    border-radius: 24px;
  }
</style>