<script setup type="module">
import axios from 'axios'
import { onMounted,reactive } from 'vue';

let jsonData =reactive({code:1,content:'你是别人眼中的小恶魔，却是我心中的大天使。'})

let getLoveMessage =()=>{
  axios({
    method:"post", // 请求方式
    url:"https://api.uomg.com/api/rand.qinghua?format=json",  // 请求的url
    data:{ // 当请求方式为post时,data下的数据以JSON串放入请求体,否则以key=value形式放url后
      username:"123456"
    }
  }).then( function (response){//响应成功时要执行的函数
    console.log(response)
    Object.assign(jsonData,response.data)
  }).catch(function (error){// 响应失败时要执行的函数
    console.log(error)

    // 本地备用内容
    const localMessages = ["不要抱怨，抱我。",
      "近朱者赤，近你者甜。",
      "我是九你是三，除了你还是你。",
      "你知道我的缺点是什么吗? 是缺点你。",
      "最近有谣言说我喜欢你，我要澄清一下，那不是谣言。",
      "我怀疑你的本质是一本书，不然为什么让我越看越想睡。",
      "我发现昨天很喜欢你，今天也很喜欢你，而且有预感明天也会喜欢你。",
      "“我觉得你这个人不适合谈恋爱” “为什么?” “适合结婚。”",
      "你知道你和星星有什么区别吗?星星在天上，你在我心里。",
      "“你最近是不是又胖了?” “没有啊，为什么这么说?” “那为什么在我心里的分量越来越重了?”",
      "这是我的手背，这是我的脚背，你是我的宝贝。",
      "猜猜我的心在哪边?左边。错了，在你那边。",
      "听闻先生治家有方，小女余生愿闻其详",
      "你闻到什么味道了吗?没有啊！怎么你一出来空气都是甜的了。",
      "“我想买一块地。”“什么地?”“你的死心塌地。”",
      "“你累不累啊?”“不累。”“可是你都在我脑里跑了一天了！”",
      "“你能不能闭嘴?”“我没有说话啊”“那为什么我满脑子都是你的声音?”",
      "“你知道我为什么感冒了吗?”“因为着凉了?”“不，因为我对你完全没有抵抗力。”",
      "甜有100种方式，吃糖，蛋糕，还有每天98次的想你",
      "从今以后我只能称呼你为您了，因为，你在我心上。",
      "莫文蔚的阴天，孙燕姿的雨天，周杰伦的晴天，都不如你和我聊天。",
      "你有没有问到什么烧焦的味道?那是我的心在燃烧。",
      "“你为什么要害我?”“害你什么?”“害我那么喜欢你!”",
      "我对你的爱，就像拖拉机上山，轰轰烈烈……",
      "“游乐园那个，可以骑在上面的”“有音乐的叫旋转什么?”“木马。”“mua”",
      "“面对你，我不仅善解人意，我还善解人衣。”",
      "你喜欢喝水吗?那你已经喜欢上70%的我了。",
      "“既然你把我的心已经弄乱了，那你打算什么时候来弄乱我的床?”",
      "你上辈子一定是碳酸饮料吧，为什么我一看到你就能开心的冒泡。",
      "三十晚上的鞭炮再响，都没有我想想你那么想。",
      "我想去取一下东西，你等一下，我来娶你了。",
      "别让我看见你，不然我见你一次，就喜欢你一次。",
      "你知道你像什么人吗?(什么人?)我的女人。",
      "你近视吗?(不近视啊)那你怎么看不出我喜欢你。",
      "现在几点了?(12点)不，是我们幸福的起点。",
      "把你的名字写在烟上吸进肺里，让你保持在离我心脏最近的地方。",
      "我生在南方，活在南方，栽在你手里，总算是去过不一样的地方。",
      "我想吃碗面 什么面 你的心里面。",
      "你可以帮我个忙么? 什么忙? 帮忙快点爱上我!",
      "“你是哪里人” “池州人” “不，你是我的心上人。”"];

    // 随机选择一个本地内容
    const randomIndex = Math.floor(Math.random() * localMessages.length);
    jsonData.content = localMessages[randomIndex];
  })
}

const themes = ['light-theme', 'pink-theme', 'blue-theme', 'green-theme', 'yellow-theme', 'purple-theme', 'image-theme'];
let currentThemeIndex = -1; // -1 表示默认深色主题

const toggleTheme = () => {
  const root = document.documentElement;

  // 移除所有主题类
  themes.forEach(theme => root.classList.remove(theme));

  // 切换到下一个主题
  currentThemeIndex = (currentThemeIndex + 1) % (themes.length + 1);

  // 如果不是默认主题（-1），则添加相应的主题类
  if (currentThemeIndex >= 0) {
    root.classList.add(themes[currentThemeIndex]);
  }
}

/* 通过onMounted生命周期,自动加载一次 */
onMounted(()=>{
  getLoveMessage()
  document.documentElement.style.setProperty('--bg-image', 'url("https://yydwjj.github.io/map/backgroud.png")');
})
</script>

<template>
  <div class="container">
    <h1>{{jsonData.content}}</h1>
    <div class="button-group">
      <button @click="getLoveMessage">~</button>
      <button @click="toggleTheme">-</button>
    </div>
  </div>
</template>

<style scoped>
</style>