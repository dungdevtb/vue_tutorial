<script>
export default {
  name: "AboutTutorial",
  props: {
    // msg: String,
  },
};
</script>

<script setup>
import { ref, reactive, computed } from "vue";

const isShow = ref(true);
const toggle = () => {
  isShow.value = !isShow.value;
};

const textInput = ref("");
// console.log(textInput);

// v-for
let id = 0;
const newTodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: id++, text: "Learn HTML", done: true },
  { id: id++, text: "Learn JavaScript", done: true },
  { id: id++, text: "Learn Vue", done: false },
]);

// console.log(todos.value);

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

const addTodo = () => {
  // sử dụng push để đẩy ptu ms vào mảng
  todos.value.push({ id: id++, text: newTodo.value, done: false });
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

const myObject = reactive({
  title: "How to do lists in Vue",
  author: "Jane Doe",
  publishedAt: "2016-04-10",
});

// vòng lặp lồng nhau
const sets = ref([
  [1, 2, 3, 4, 5],
  [6, 7, 8, 9, 10],
]);

const even = (numbers) => {
  return numbers.filter((number) => number % 2 === 0);
};
</script>

<template>
  <div class="about-container">
    <!-- v-if -->
    <div class="v-if-container">
      <div class="toggle">
        <h3>Các hàm điều kiện v-if v-else</h3>
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
      <div>
        <h3>Vòng lặp v-for</h3>
        <form action="">
          <input type="text" v-model="newTodo" @keydown="onEnterAdd" />
          <button @click="addTodo">Add Todo List</button>
        </form>
        <ul>
          <li v-for="(item, index) in todos" :key="item.id">
            {{ index + 1 }} - {{ item?.text }}
            <button @click="removeTodo(item)">X</button>
          </li>
        </ul>
      </div>
      <div>
        <h3>v-for in Object</h3>
        <ul>
          <li v-for="(value, key, index) in myObject" :key="value">
            <div>{{ value }}</div>
            {{ index + 1 }}. {{ key }}: {{ value }}
          </li>
        </ul>
      </div>
      <div>
        <h3>vòng lặp in 10 số</h3>
        <!-- vòng lặp in 10 số -->
        <span v-for="n in 10" :key="n">{{ n }} &nbsp;</span>
      </div>
    </div>

    <div class="example">
      <div>
        <h3>show Todo list có checkbox done</h3>
        <form action="" @submit.prevent="addTodo">
          <input v-model="newTodo" />
          <button>Add Todo</button>
        </form>
        <ul>
          <li v-for="todo in filteredTodos" :key="todo?.id">
            <input type="checkbox" v-model="todo.done" />
            <span :class="{ done: todo?.done }">{{ todo?.text }}</span>
            <button @click="removeTodo(todo)" style="margin-left: 15px">
              X
            </button>
          </li>
        </ul>
        <button @click="hideCompleted = !hideCompleted">
          {{ hideCompleted ? "Hiển thị tất cả" : "Ẩn những việc hoàn thành" }}
        </button>
      </div>
      <div class="v-for_nested">
        <h3>Vòng lặp lồng nhau</h3>
        <ul v-for="numbers in sets" :key="numbers">
          <li v-for="n in even(numbers)" :key="n">{{ n }}</li>
        </ul>
      </div>
      <div class="v-for_and_v-if">
        <h3>v-for and v-if</h3>
        <span v-for="n in 10" :key="n">
          <span v-if="n % 2 === 0">{{ n }} &nbsp;</span>
          <div></div>
          <span v-if="n % 2 === 1">{{ n }} &nbsp;</span>
        </span>
      </div>
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
.v-if-container,
.v-for-container,
.example {
  display: flex;
  justify-content: space-evenly;
}

.done {
  text-decoration: line-through;
}
</style>
