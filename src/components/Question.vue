<template>
  <div class="question-wrapper">
    <h2 class="title">{{data.text}}</h2>

    <div class="answers">
      <div 
        v-for="(answer, index) in data.answers"
        :class="`card answer ${answer === selected ? 'selected' : ''}`"
        :key="index"
        @click="() => select(answer)"
      >
        <p class="answer-text">{{answer}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true
    },
    update: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      selected: null,
    };
  },
  methods: {
    select (answer) {
      this.selected = answer;
      this.update(answer)
    }
  }
};
</script>

<style lang="css" scoped>
.question-wrapper {
  padding: 0% 20%;
}

.title {
  text-align: center;
  margin-bottom: 32px;
}

.answers {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 32px;
}

.answer {
  display: flex;
  flex-direction: row;
}

.answer-text {
  flex: 1;
  text-align: center;
  align-content: center;
  cursor: pointer;
  color: var(--text-light);
  font-weight: bold;
}

.selected {
  background-color: var(--secondary);
}

@media only screen and (max-width: 600px){
  .question-wrapper {
    padding: 0 0%;
  }
}
</style>
