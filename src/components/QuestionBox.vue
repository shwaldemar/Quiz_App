<template>
  <div class="question-box-container">
    <div>
    <b-jumbotron>
      <template slot:lead>
        {{currentQuestion.question}}
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item v-for="(answer, index) in answers" :key="index">{{answer}}</b-list-group-item>
      </b-list-group>
      <!-- <p v-for="(answer, index) in answers" :key="index">{{answer}}</p> -->

      <b-button variant="primary" href="#">Submit Answer</b-button>
      <b-button @click="next" variant="success" href="#">Next Question</b-button>
    </b-jumbotron>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currentQuestion: Object,
    next: Function,
  },
  computed: {
    answers(){
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      return answers
    }
  }
}
</script>

<style lang="css" scoped>
</style>
