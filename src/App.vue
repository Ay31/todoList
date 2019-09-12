<template>
  <div class="main">
    <InputArea></InputArea>
    <Prepare></Prepare>
    <Accomplish></Accomplish>
  </div>
</template>

<script>
import InputArea from "./components/InputArea.vue";
import Prepare from "./components/Prepare.vue";
import Accomplish from "./components/Accomplish.vue";

export default {
  name: "app",
  components: {
    InputArea,
    Prepare,
    Accomplish
  }
};
</script>

<style>
* {
  background: #ccc;
}
</style>
