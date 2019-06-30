<template>
  <div id="question-box">
    <b-jumbotron>
      <template slot="lead">
        Some question?
      </template>

      <hr class="my-4" />

      <p>
        List of answers
      </p>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" href="#">Next question</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  name: "QuestionBox"
};
</script>

<style scoped>
</style>
