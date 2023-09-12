<script>
export default {
  name: "LifeCycle",
  props: {},
};
</script>

<script setup>
import { ref, onMounted, onUpdated, onUnmounted } from "vue";

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
</script>

<template lang="">
  <div class="vue_container">
    <h3>Life Cycle VUE</h3>
    <p ref="pElementRef">hello</p>

    <h3>onUpdated</h3>
    <button id="count" @click="count++">{{ count }}</button>

    <h1></h1>
  </div>
</template>

<style lang=""></style>
