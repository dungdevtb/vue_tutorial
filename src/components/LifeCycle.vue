<script>
export default {
  name: "LifeCycle",
  props: {},
};
</script>

<script setup>
import { ref, onMounted, onUpdated, onUnmounted, watch } from "vue";

//Creation - Được chạy khi component của bạn được khởi tạo
//onMounted: các element đã được hiển thị và khai báo cho phép truy cập DOM
// ref được truy cập sau khi component 'mounted'
const pElementRef = ref(null);
onMounted(() => {
  setTimeout(() => {
    console.log("Element is Mounted");
    pElementRef.value.textContent = "mounted!";
  }, 3000);
});

//onUpdated - Được gọi khi data được thay đổi,DOM đươc cập nhật
const count = ref(0);
onUpdated(() => {
  // text content should be the same as current count.value
  console.log("Element onUpdated");
  console.log(document.getElementById("count").textContent);
});

//onUnmounted - sử dụng khi ko muốn thục thi 1 element nào đó
let intervalId;
onMounted(() => {
  intervalId = setInterval(() => {
    console.log("abcdefgjh");
  }, 2000);
});

onUnmounted(() => {
  console.log("Element Unmounted");
  clearInterval(intervalId);
});

// -------------------------------
// WATCHER
const todoId = ref(1);
const todoData = ref(null);
const fetchData = async () => {
  todoData.value = null;
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  );
  todoData.value = await res.json();
};

fetchData();
watch(todoId, fetchData);
// đối số đầu tiên của watch là 1 đối tượng cần theo dõi có thể là :ref, reactive obj, hàm ,....
</script>

<template lang="">
  <div class="vue_container">
    <div class="life_cycle">
      <h3>Life Cycle VUE</h3>
      <p ref="pElementRef">hello</p>

      <h3>OnUpdated</h3>
      <button id="count" @click="count++">{{ count }}</button>
    </div>

    <div class="watcher">
      <h3>Watcher</h3>
      <p>Todo Id: {{ todoId }}</p>
      <button @click="todoId++">Fetch next todo:</button>
      <p v-if="!todoData">Loading...</p>
      <p v-else>{{ todoData }}</p>
    </div>
  </div>
</template>

<style lang="scss">
.vue_container {
  display: flex;
  justify-content: space-evenly;
}
</style>
