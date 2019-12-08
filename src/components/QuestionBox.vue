<template>
  <div class="question-box-container">
    <div>
    <b-jumbotron>
      <template slot:lead>
        Questions from the API will render here.
      </template>

      <hr class="my-4">

      <p>
        Answer options from the API will render here.
      </p>

      <b-button variant="primary" href="#">Submit Answer</b-button>
      <b-button variant="success" href="#">Next Question</b-button>
    </b-jumbotron>
    </div>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="css" scoped>
</style>
