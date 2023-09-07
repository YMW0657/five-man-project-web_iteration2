<template>
  <div class="quiz">
    <div class="quiz-wrapper">
      <a-progress :percent="((actions.quizIndex+1)*100)/12" />
      <div class="progress"><span>{{ actions.quizIndex + 1 }}</span>/<span>12</span></div>
      <div class="title">{{ actions.quizIndex+1 +"、"+ ourQuizs[actions.quizIndex].question }}</div>
      <div class="option">
        <ul>
          <li
            v-for="item in ourQuizs[actions.quizIndex].options"
            :key="item.value"
            v-html="item.label"
            @click="actions.selectFn(item)"
            :class="item.value==ourQuizs[actions.quizIndex].yourAnswer?'selected':''">
          </li>
        </ul>
          <!-- <a-radio-group v-model:value="ourQuizs[actions.quizIndex].yourAnswer">
            <a-radio
              :style="radioStyle"
              :value="item.value"
              v-for="item in ourQuizs[actions.quizIndex].options"
              :key="item.id"
            >
              {{ item.label }}
            </a-radio>
          </a-radio-group> -->
      </div>
      <div class="direction">
        <a-button 
          type="primary" 
          class="prev" 
          :disabled="!actions.quizIndex" 
          @click="actions.prevFn">
          <template #icon>
            <LeftOutlined />
          </template>
        </a-button>
        <a-button 
          type="primary" 
          class="next" 
          :disabled="actions.quizIndex==11" 
          @click="actions.nextFn">
            <template #icon>
              <RightOutlined />
            </template>
          </a-button>
        <a-button type="primary" class="result" v-if="actions.quizIndex==11" @click="actions.showResult" :loading="actions.loading">{{actions.loading?"calculating...":"Result"}}</a-button>
      </div>
    </div>
    <!-- <div class="selection">
      <a-button type="primary" v-for="item in ourQuizs[actions.quizIndex].options" :key="item.id">{{ item.label.slice(3, 4) }}</a-button>
    </div> -->
  </div>
  <!-- <a-modal v-model:open="model.visible" class="answer-model" title="Result" width="700px" ok-text="Confirm" cancel-text="Close" @cancel="model.hideModal" @ok="model.hideModal"> -->
  <div v-if="model.visible" class="answer-model-shadow">
    <div class="answer-model">
      <div class="model-title">
        Result
      </div>
      <div class="model-answer-content">
        There are a total of <b>{{ result.total }}</b>
        questions, you answered <b>{{ result.corrent }}</b> 
        of them correctly with an <br /> accuracy rate of <b>{{(result.corrent*100/result.total).toFixed(0)}}%</b>.
      </div>
      <div class="model-lists">
        <div class="model-list" v-for="item in result.lists" :key="item.type">
          <b>For {{item.name}} scam types:</b> <b>{{ item.total }}</b> questions in total, <b>{{ item.correctTotal }}</b> answered correctly. </div>
      </div>
      <div class="model-conclusion">
        <b>Conclusion: </b>
        <span v-if="result.lists.filter(item=>!item.isGood).map(item=>item.name).length">You made more mistakes in the <span class="danger">{{result.lists.filter(item=>!item.isGood).map(item=>item.name).join(" and ")}}</span> scam category, It's recommended that you study more about this topic </span>
        <span v-if="result.lists.filter(item=>!item.isGood).map(item=>item.name).length&&result.lists.filter(item=>item.isGood).map(item=>item.name).length">,</span>
        <span v-if="result.lists.filter(item=>item.isGood).map(item=>item.name).length">You performed perfectly in the <span class="success">{{result.lists.filter(item=>item.isGood).map(item=>item.name).join(" and ")}}</span> categories, please keep it up.</span>
      </div>
      <div class="btn-group">
        <a-button type="primary" @click="model.hideModal">Confirm</a-button>
      </div>
    </div>
  <!-- </a-modal> -->
  </div>
</template>
<script setup>
  import { reactive, ref, onMounted } from 'vue';
  import { quizs, getRandomElementsFromArray } from "../utils/index"
  import { message } from 'ant-design-vue';
  import { LeftOutlined, RightOutlined} from '@ant-design/icons-vue';
  import axios from "axios";
  const radioStyle = reactive({
    display: 'flex',
    height: '30px',
    lineHeight: '30px',
  });
  const types = [4, 4, 4];
  const max = types.reduce((prev,next)=>prev+next);
  //const typeMaps = ["Email", "Phishing", "SMS", "Elder"];
  const typeMaps = ["Phishing", "Spoofing", "Card theft"];
  const ourQuizs = ref([{}]);
  const result = reactive({
    lists: [],
    total: max,
    corrent: 0,
  });

  const actions = reactive({
    loading:false,
    quizIndex:0,
    prevFn:()=>{
      actions.quizIndex--;
      if(actions.quizIndex===ourQuizs.length){
        return;
      }
    },
    nextFn:()=>{
      const yourAnswer = ourQuizs.value[actions.quizIndex].yourAnswer;
      if(!yourAnswer){
        message.warning('Please select the answer!');
        return;
      }
      actions.quizIndex++;
      if(actions.quizIndex===0){
        return;
      }
    },
    selectFn:(item) => {
      ourQuizs.value[actions.quizIndex].yourAnswer = item.value;
    },
    showResult:()=>{
      const yourAnswer = ourQuizs.value[actions.quizIndex].yourAnswer;
      if(!yourAnswer){
        message.warning('Please select the answer!');
        return;
      }
      result.corrent = 0
      result.lists = types.map((item,index)=>{
        result.corrent += ourQuizs.value.filter(item=>item.type==(index+1)).filter(item=>item.correct==item.yourAnswer).length
        return {
          type:index+1,
          name:typeMaps[index],
          total: item,
          correctTotal: ourQuizs.value.filter(item=>item.type==(index+1)).filter(item=>item.correct==item.yourAnswer).length,
          isGood:item == ourQuizs.value.filter(item=>item.type==(index+1)).filter(item=>item.correct==item.yourAnswer).length
        }
      })
      actions.loading=true
      setTimeout(()=>{
        model.showModal()
        actions.loading=false
      },2000)
    }
  });
  const model = reactive({
    visible:false,
    showModal:()=>{
      model.visible = true;
    },
    hideModal:()=>{
      model.visible = false;
      result.lists = [];
      result.total = max;
      result.corrent = 0;
      actions.quizIndex = 0;
      ourQuizs.value.forEach(item=>{
        item.yourAnswer = ""
      })
    }
  })
  onMounted(() => {
    axios.get('/api/quiz/getquizpool')
    .then(function (response) {
      console.log(response.data);
      if(response.data.code==200){
        const lists=response.data.data
        lists.forEach(item=>{
          item.yourAnswer="";
          console.log(item.id);
          item.options = JSON.parse(item.options);
        })
        ourQuizs.value = []
        types.forEach((type, index)=>{
          const myTypeItem = lists.filter(item=>item.type==(index+1))
          const selects = getRandomElementsFromArray(myTypeItem, type)
          ourQuizs.value.push(...selects);
        })
        ourQuizs.value.sort((a,b)=>{
          return a.id-b.id
        })
        console.log(ourQuizs.value);
      }else{
        ourQuizs.value=[]
      }
    })
  })
</script>
<style scoped>
  .quiz{
    background-color: #efefef;
    height: calc(100vh - 64px);
    padding:30px;
  }
  .quiz-wrapper{
    display: flex;
    flex-direction: column;
    width: 1000px;
    margin:0 auto;
    background-color: #fff;
    padding:24px 30px;
    border-radius: 8px;
  }
  .quiz-wrapper .progress{
    text-align: center;
    margin-bottom: 20px;
    font-size: 30px;
    letter-spacing: 1px;
  }
  .quiz-wrapper .progress span{
  }
  .title{
    font-size: 24px;
    line-height: 36px;
  }
  .option {
    margin-top: 20px;
    align-self: flex-start;
  }
  .option ul,.option li{
    list-style: none;
    margin:0;
    padding:0;
  }
  .option li {
    font-size: 16px;
    line-height: 20x;
    cursor: pointer;
    margin: 12px 0;
    padding: 8px;
    border-radius: 8px;
    min-width: 400px;
    border: 1px solid #d9d9d9;
    background-color: rgba(0, 0, 0, 0.06);
  }
  .option li.selected{
    background-color: #b926f8;
    color: #fff;
  }
  .direction{
    margin-top: 50px;
  }
  .direction .next{
    margin-left: 20px;
  }
  .direction .result{
    margin-left: 20px;
  }
  .selection{
    width: 1000px;
    margin: 30px auto 0;
    display: flex;
    justify-content: center;
  }
  .selection button{
    margin-left: 30px;
    width: 140px;
  }
  .selection button:nth-child(1){
    margin-left: 0;
    background-color: #58e442;
  }
  .selection button:nth-child(1):hover{
    background-color: #4cc03a;
  }
  .selection button:nth-child(2){
    background-color: #ca4e46;
  }
  .selection button:nth-child(2):hover{
    background-color: #ac443c;
  }
  .selection button:nth-child(3){
    background-color: #9b7a36;
  }
  .selection button:nth-child(3):hover{
    background-color: #7e632d;
  }
  .selection button:nth-child(4){
    background-color: #469aca;
  }
  .selection button:nth-child(4):hover{
    background-color: #3b80a8;
  }

  .answer-model-shadow{
    width: 100%;
    height: 100%;
    position: fixed;
    left:0;
    top: 0;
    right: 0;
    bottom: 0;
    z-index: 999;
    background-color: rgba(0, 0, 0, 0.4);
  }
  .answer-model .model-title{
    font-size: 24px;
    color: #135592;
    font-weight: bold;
  }
  /* .answer-model .ant-modal-title{
    font-size: 28px;
    font-weight: 600;
    color: #222C28;
  }
   */
  .answer-model{
    background-color: #fff;
    width: 700px;
    min-height: 350px;
    border-radius: 4px;
    z-index: 1000;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    padding: 30px;
    color: #000;
    font-size: 16px;
    line-height: 24px;
  }
  .answer-model .btn-group{
    padding-top: 30px;
  }
  .answer-model .btn-group button{
    margin: 0 auto;
    display: block;
    width: 140px;
    letter-spacing: 1px;
    background-color: #135592;
  }
  .answer-model .btn-group button:hover{
    background-color: #1a6cb9;
  }
  .model-answer-content{
    font-size: 16px;
    margin-top: 12px;
    margin-bottom: 8px;
    color: #222C28;
  }
  .model-lists .model-list{
    line-height: 28px;
    color: #222C28;
    font-size: 14px;
  }
  .model-conclusion{
    margin-top: 12px;
    line-height: 28px;
    color: #222C28;
    font-size: 16px;
  }
  .model-conclusion .success{
    color: #20A675;
  }
  .model-conclusion .danger{
    color: #ff4d4f;
  }

</style>
<style>
:where(.css-dev-only-do-not-override-1ugq3w3).ant-progress .ant-progress-text{
  display: none;
}
</style>