<script>
export default {
  name: "ChildEvent",
};
</script>

<script setup>
import { defineEmits } from "vue";
//định nghĩa sự kiện Emit
const emit = defineEmits(["propChild"]); //propCHild: name event
//emit with argument
emit("propChild", "I am prop in Child");
</script>

<template lang="">
  <div>
    <h3>Child Component</h3>

    <button @click="$emit('increaseBy', 1)">Increase by 1</button>
    <!-- <button @click="$emit('increaseBy', 1)">Decrease by 1</button> -->
  </div>
</template>

<style lang=""></style>
