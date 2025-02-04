<template>
  <div class="app">
    <div class="wrapper">
      <Quiz :questions=questions disableBack />
    </div>
  </div>
</template>

<script>
import Quiz from "./components/Quiz.vue";
import questions from "./data/questions";

export default {
  components: { Quiz },
  data() {
    return { questions: questions }
  } 
}
</script>

<style lang="css" scoped>
.app {
  height: 100vh;
  display: flex;
  background-color: var(--background);
}

.wrapper {
  flex: 1;
  padding: 16px 64px;
}

/* mobile */
@media only screen and (max-width: 600px){
  .wrapper {
    padding: 16px 8px;
  }
}
</style>
