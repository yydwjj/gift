<script setup type="module">
import axios from 'axios'
import { onMounted,reactive } from 'vue';

let jsonData =reactive({code:1,content:'我努力不是为了你而是因为你'})

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
  document.documentElement.style.setProperty('--bg-image', 'url("https://yydwjj.github.io/map/b2ade726a62615e5883048edc845e03.jpg")');
})
</script>

<template>
  <div class="container">
    <h1>{{jsonData.content}}</h1>
    <div class="button-group">
      <button @click="getLoveMessage">~</button>
      <button @click="toggleTheme">切换主题</button>
    </div>
  </div>
</template>

<style scoped>
</style>