<script>
// import { ref } from "vue";

export default {
  // setup() {
  //   const count = ref(0);

  //   function increment() {
  //     count.value++;
  //   }

  //   return {
  //     count,
  //     increment,
  //   };
  // },

  name: "HelloWorld",
  props: {
    msg: String,
  },
};
</script>

<script setup>
import { ref, reactive } from "vue";

const count = ref(0); //tương tư ref react
function increment() {
  count.value++;
}
const message = reactive({ msg: "BayyyyMaxxxx!" }); //reactive: thường đk dùng để gán biến số chuỗi

const text = ref("");
const handlePrintText = (e) => {
  text.value = e.target.value;
};
</script>

<template>
  <img alt="Vue logo" src="../assets/logo.png" />
  <div class="hello">
    <h1>Welcome to Your Vue.js App</h1>
    <h3>Message Reactive: {{ message.msg }}</h3>
  </div>
  <div class="count_container">
    <button @click="count--">Giảm dần</button>
    <span>{{ count }}</span>
    <button @click="increment">Tăng dần</button>
  </div>

  <div class="">
    <div class="v-bind v-on">
      <!-- v-bind:value = :value -->
      <div>Kết hợp v-bind và v-on sẽ tạo đk liên kết 2 chiều</div>
      <input :value="text" @input="handlePrintText" placeholder="Type here" />
      <p>{{ text }}</p>
    </div>
    <div class="v-model">
      <div>v-model= v-bind + v-on</div>
      <input v-model="text" placeholder="Type here" />
      <p>{{ text }}</p>
    </div>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.count_container {
  display: flex;
  justify-content: space-evenly;
  align-items: center;

  button {
    width: 100px;
    height: 50px;
    border-radius: 12px;
  }
}
</style>
