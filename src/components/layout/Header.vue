<template>
  <div id="header">
    <b-nav tabs>
      <b-nav-item disabled><strong>Quizz App</strong></b-nav-item>
      <b-nav-item disabled><strong>Correct answers: {{correctAnswers}}/{{numTotal}} </strong></b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props:{
    correctAnswers: 0,
    numTotal: 0
  }
};
</script>

<style>

</style>
