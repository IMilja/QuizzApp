<template>
  <div id="question-box">
    <b-jumbotron>
      <template slot="lead">{{currentQuestion.question}}</template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          v-bind:key="index"
          v-on:click="selectAnswer(index)"
          v-bind:class="correctClass(index)"
        >{{answer}}</b-list-group-item>
      </b-list-group>

      <b-button
        variant="primary"
        v-on:click="submitAnswer"
        v-bind:disabled="selectedIndex === null || answered"
      >Submit</b-button>
      <b-button v-on:click="next" variant="success">Next question</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  name: "QuestionBox",
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      answered: false,
      shuffledAnswers: []
    };
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.shuffleAnswers();
        this.answered = false;
      }
    }
  },
  computed: {
    answers(e) {
      e.preventDefault;
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    submitAnswer() {
      let isCorrect = false;
      this.answered = true;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.increment(isCorrect);
    },
    correctClass(index) {
      if (!this.answered && this.selectedIndex === index) {
        return "selected";
      } else if (this.answered && this.correctIndex === index) {
        return "correct";
      } else if (
        this.answered &&
        this.correctIndex !== index &&
        this.selectedIndex === index
      ) {
        return "wrong";
      }
    }
  }
};
</script>

<style scoped>
.list-group {
  margin-bottom: 10px;
}

.list-group-item:hover {
  background: #d1d1d1;
  cursor: pointer;
}

.btn {
  margin: 0 5px;
}

.selected {
  background: lightblue;
}

.correct {
  background: lightgreen;
}

.wrong {
  background: lightcoral;
}
</style>
