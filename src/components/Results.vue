<template>
  <div class="results-wrapper">
    <h2>Results</h2>

    <div class="results">
      <div class="card results-card" v-for="(key, index) in Object.keys(data)" :key="index">
        <div class="results-question">{{key}}</div>
        <div class="results-answer">{{data[key]}}</div>
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
  },
  data() {
    return {};
  },
};
</script>

<style lang="css" scoped>
.results-wrapper {
  padding: 0 20%;
}

.results {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 32px;
}

.title {
  text-align: center;
}

.results-card {
  align-content: center;
  cursor: default;
}

.results-question {
  text-align: center;
  margin-bottom: 8px;
  font-size: 0.8em;
  color: var(--text-light)
}

.results-answer {
  text-align: center;
  font-weight: bold;
  font-size: 1.2em;
  color: var(--text-dark)
}

/* mobile */
@media only screen and (max-width: 600px){
  .results-wrapper {
    padding: 0 0%;
  }
}
</style>