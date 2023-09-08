<script>
export default {
  name: "AboutTutorial",
  props: {
    // msg: String,
  },
};
</script>

<script setup>
import { ref } from "vue";

const isShow = ref(true);
const toggle = () => {
  isShow.value = !isShow.value;
};

const textInput = ref("");
// console.log(textInput);

// v-for
let id = 0;
const newTodo = ref("");
const todos = ref([
  { id: id++, text: "Learn Html" },
  { id: id++, text: "Learn JavaScript" },
  { id: id++, text: "Learn Vue" },
]);
const addTodo = () => {
  // sử dụng push để đẩy ptu ms vào mảng
  todos.value.push({ id: id++, text: newTodo.value });
  // sau khi ấn thêm ms thì input sẽ trống
  newTodo.value = "";
  console.log(todos.value);
};

const onEnterAdd = (e) => {
  if (e.keyCode === 13) {
    addTodo();
  }
};

const removeTodo = (item) => {
  //sử dụng filter để tạo mảng ms
  // todos.value=todos.value.filter((new)=> new!==item)
  //ko sử dụng tên new để đặt tên cho vòng lặp vì sẽ trùng tên biến new: tạo đối tượng ms
  todos.value = todos.value.filter((t) => t !== item);
};
</script>

<template>
  <div class="about-container">
    <!-- v-if -->
    <div class="v-if-container">
      <h3>Các hàm điều kiện v-if v-else</h3>
      <div class="toggle">
        <button @click="toggle">Btn Toggle</button>
        <p v-if="isShow">Show True</p>
        <p v-else>Show False</p>
      </div>
      <div class="showText">
        <h3 style="margin-bottom;: 15px">
          Nhập a Hiện A, nhập b sẽ hiện B , nhập c sẽ hiện C, nhập khác hiện
          những j nhập
        </h3>
        <input v-model="textInput" />
        <p v-if="textInput === 'a'">A</p>
        <p v-else-if="textInput === 'b'">B</p>
        <p v-else-if="textInput === 'c'">C</p>
        <p v-else>{{ textInput }}</p>
      </div>
    </div>
    <!-- v-for -->
    <div class="v-for-container">
      <h3>Vòng lặp v-for</h3>
      <form action="">
        <input type="text" v-model="newTodo" @keydown="onEnterAdd" />
        <button @click="addTodo">Add Todo List</button>
      </form>
      <ul>
        <li v-for="item in todos" :key="item.id">
          {{ item?.text }}
          <button @click="removeTodo(item)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<!-- STYLE -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
</style>
