<template>
  <div id="app">
    <Header 
    v-bind:correctAnswers="correctAnswers"
    v-bind:numTotal="numTotal"
    />
    <b-container>
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox 
            v-if="questions.length"
            v-bind:currentQuestion="questions[index]"
            v-bind:next="next"
            v-bind:increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/layout/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";
import axios from 'axios';

export default {
  name: "app",
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      correctAnswers: 0,
      numTotal: 0,
    }
  },
  methods:{
    next: function (){
      this.index += 1;
    },
    increment: function(isCorrect){
      if(isCorrect){
        this.correctAnswers += 1;
      }
      this.numTotal += 1;
    }
  },
  mounted: function () {
    axios.get("https://opentdb.com/api.php?amount=10&category=18&type=multiple")
    .then(res => this.questions = res.data.results)
    .catch(err => console.log(err));
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
