<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="Aweseome things happens!" />
    </div>
  </header>

  <div>
    <h2>Submit a sentence for Sentiment Analysis</h2>
    <input type="text" v-model="sentence" placeholder="Enter your sentence here...">
    <button @click="analyzeSentence">Analyze</button>
    <div v-if="result" :class="result.score > 0 ? 'positive' : 'negative'">
      <p>{{ result.score > 0 ? 'Positive' : 'Negative' }} sentiment</p>
      <p>{{ result.score }}</p>
    </div>
  </div>
</template>


<script>
  import Sentiment from 'sentiment';

  export default {
    data() {
      return {
        sentence: '',
        result: null
      };
    },
    methods: {
      analyzeSentence() {
        const sentiment = new Sentiment();
        this.result = sentiment.analyze(this.sentence);
      }
    }
  };
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.positive {
  color: green;
}
.negative {
  color: red;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
