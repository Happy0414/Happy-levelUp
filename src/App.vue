<script setup lang="ts">
import { ref, computed } from 'vue'

type inputData = {
  id: number;
  title: string;
  exp: number;
}

const level = ref(1);
const datas = ref<inputData[]>([]);
const title = ref('');
const exp = ref(0);

const addData = () => {
  const trimTitle = title.value.trim();
  if(trimTitle === '') return;
  
  const newData: inputData = {
    id: Date.now(),
    title: trimTitle,
    exp: exp.value
  }

  datas.value.push(newData);
  title.value='';
  
}

const levelClass = computed(() => {
  if(level.value >= 100){return 'gold'};
  if(level.value >= 90){return 'purple'};
  if(level.value >= 80){return 'red'};
  if(level.value >= 60){return 'orange'};
  if(level.value >= 40){return 'yellow'};
  if(level.value >= 20){return 'blue'};
  return 'green';
})
</script>

<template>
<h1>Happy-level-up</h1>
<h2>Level：<span :class="levelClass">{{ level }}</span></h2>
<input v-model="title" placeholder="経験を入力" /><br>

<input v-model="exp" type="number" min="1" max="100" />
<span>0~100</span>
<button @click="addData">追加</button>
<ul>
  <li v-for="data in datas" key: data.id>
    <div class="data">
      <span>内容：</span>{{ data.title }}<br>
      <span>経験値：</span>{{ data.exp }}
    </div>
  </li>
</ul>
</template>

<style scoped>
.data{
  border: solid 1.5px;
  border-radius: 15px;
}

.green{ color: green; }
.blue{ color: blue; }
.yellow{ color: yellow; }
.orange{ color: orange; }
.red{ color: red; }
.purple{ color: purple; }
.gold{ color: gold; }

</style>
