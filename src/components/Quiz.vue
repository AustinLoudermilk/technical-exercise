<template>
  <div class="container">
    <div class="step">
      <div v-if="!finished">
        <span>{{ step + 1 }}</span> 
        of <span>{{ questions.length }}</span>
      </div>
    </div>

    <div class="content-container">
      <Question
        v-if="!finished"
        :data=questions[this.step]
        :update="update"
      />
      <Results v-else :data="answers" />
    </div>

    <div v-if="this.error" class="error">
      {{ this.error }}
    </div>

    <div class="controls">
      <div v-if="!finished">
        <button class="btn" v-if="!disableBack" @click="prev">prev</button>
        <button class="btn" v-if="!(step >= questions.length - 1)" @click="next">next</button>
        <button class="btn" v-else @click="submit">submit</button>
      </div>
      <div v-else>
        
      </div>
    </div>
  </div>
</template>

<script>
import Question from "./Question.vue";
import Results from "./Results.vue";

export default {
  components: { Question, Results },
  props: {
    questions: {
      type: Array,
      required: true
    },
    disableBack: {
      type: Boolean,
      required: false
    }
  },
  data() {
    return {
      step: 0,
      finished: false,
      error: null,
      answers: {}
    };
  },
  methods: {
    validate () {
      const valid = this.questions[this.step].text in this.answers;
      this.error = !valid ? "Please select an answer" : null;
      return valid;
    },
    next () {
      if (this.step >= this.questions.length - 1) return;
      if (!this.validate()) return;

      this.step++;
    },
    prev () {
      if (this.disableBack || this.step <= 0) return;
      this.step--;
    },
    update (answer) {
      const key = this.questions[this.step].text;
      this.answers[key] = answer;
      this.validate();
    },
    submit () {
      if (!this.validate()) return;
      this.finished = true
    },
  }
};
</script>

<style lang="css" scoped>
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.content-container {
  flex: 1
}

.step {
  text-align: center;
  height: 10%;
  color: var(--text-dark);
}

.error {
  text-align: center;
  padding: 32px;
  color: var(--error);
  font-weight: bold;
}

.controls {
  flex-direction: row;
  align-self: center;
  height: 10%;
}
</style>
