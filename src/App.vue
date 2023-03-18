<template>
  <div id="app">
    <Header :index="index" :numCorrect="numCorrect" :numTotal="numTotal" />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Content
            v-if="questionlist.length"
            :cQuestion="questionlist[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";

export default {
  name: "App",
  components: {
    Header,
    Content,
  },
  data() {
    return {
      questionlist: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
    };
  },
  methods: {
    next() {
      if (this.index < 9) {
        this.index++;
      }
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    },
  },
  mounted: function () {
    fetch(
      "https://opentdb.com/api.php?amount=10&category=18&difficulty=easy&type=multiple",
      {
        method: "get",
      }
    )
      .then((response) => {
        return response.json();
      })
      .then((result) => {
        this.questionlist = result.results;
      });
  },
};
</script>

<style>
</style>
