<script>
export default {
  name: "WatcherComponent",
};
</script>

<script setup>
import { ref, watch, reactive, watchEffect, watchPostEffect } from "vue";
const x = ref(0);
const y = ref(0);
// single ref
watch(x, (newX) => {
  console.log(`x is ${newX}`);
}); //theo dÕi x thay dổi x = newX
//getter
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum} `);
  }
); //hàm trả về tổng cần theo dõi = sum

// array of multiple sources
watch([x, () => y.value], ([newX, newY, Z]) => {
  console.log(`x is ${newX} and y is ${newY} ${Z}`);
}); //mảng nhìu ptu mỗi ptu ứng vs 1 ptu bên hàm
//x= newZ, ()=> y.value  =  newY,  Z chưa xác định (undefined)

const obj = reactive({ count: 1 });
watch([obj.count, () => obj.count], (reactive, getter_reactive) => {
  console.log(`reactive: ${reactive} or getter_reative: ${getter_reactive}`);
});

const todoId = ref(1);
const data = ref(null);
watch(
  todoId,
  async () => {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
    );
    data.value = await response.json();
  },
  { immediate: true }
); //imediate , muốn call back phải thực hiện ngay lập tức hàm

// watcherEffect có thể tự động theo dõi các phần phụ thuộc và gọi giá trị ngay lập tức
watchEffect(async () => {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  );
  data.value = await res.json();
});

// example watchEffect
const API_URL = `https://api.github.com/repos/vuejs/core/commits?per_page=3&sha=`;
const branches = ["main", "v2-compat"];

const currentBranch = ref(branches[0]);
const commits = ref(null);

watchEffect(async () => {
  // this effect will run immediately and then
  // re-run whenever currentBranch.value changes
  const url = `${API_URL}${currentBranch.value}`;
  commits.value = await (await fetch(url)).json();
});

console.log(commits.value);
const truncate = (v) => {
  const newline = v.indexOf("\n");
  return newline > 0 ? v.slice(0, newline) : v;
};

const formatDate = (v) => {
  return v.replace(/T|Z/g, " ");
};

// watchPostEffect: truy cập vào DOM sau khi Vue cập nhật
watchPostEffect(() => {
  /* executed after Vue updates */
  console.log("executed after Vue updates");
});
</script>

<template lang="">
  <div class="vue_container">
    <div class="example_watch">
      <h3>Example watcher: ref, array, reactive , function ,getter ...</h3>
      <div>x: <input type="text" v-model="x" /></div>
      <div>y: <input type="text" v-model="y" /></div>
      <div>{{ x + y }}</div>
    </div>
  </div>
  <div class="vue_container">
    <div class="watchEffect">
      <h3>WatchEffect</h3>
      <template v-for="branch in branches" :key="branch">
        <input
          type="radio"
          :id="branch"
          :value="branch"
          name="branch"
          v-model="currentBranch"
        />
        <label :for="branch">{{ branch }}</label>
      </template>
      <p>vuejs/vue@{{ currentBranch }}</p>
      <ul>
        <li v-for="{ html_url, sha, author, commit } in commits" :key="commit">
          <a :href="html_url" target="_blank" class="commit">
            {{ sha.slice(0, 7) }}
          </a>
          - <span class="message">{{ truncate(commit.message) }}</span
          ><br />
          by
          <span class="author"
            ><a :href="author.html_url" target="_blank">{{
              commit.author.name
            }}</a></span
          >
          at
          <span class="date">{{ formatDate(commit.author.date) }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style lang="scss">
.vue_container {
  display: flex;
  justify-content: space-evenly;
}
a {
  text-decoration: none;
  color: #42b883;
}
li {
  line-height: 1.5em;
  margin-bottom: 20px;
}
.author,
.date {
  font-weight: bold;
}
</style>
