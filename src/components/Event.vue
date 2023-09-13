<script>
export default {
  name: "EventComponent",
};
</script>

<script setup>
// Emit: truyền prop từ con lên cha
import { ref } from "vue";
import ChildEvent from "./ChildEvent.vue";

const childMsg = ref("No child msg yet!");
const count = ref(0);
</script>

<template lang="">
  <div class="event_container">
    <ChildEvent
      @prop-child="(msg) => (childMsg = msg)"
      @increase-by="(n) => (count += n)"
    />
    <!-- prop được truyền từ con lên và gán giá trị mới cho childMSg -->
    <p>{{ childMsg }}</p>
    <p>{{ count }}</p>
  </div>
</template>

<style lang="scss"></style>
