<template>
  <div class="question-box-container">
    <div>
    <b-jumbotron>
      <template slot:lead>
        {{currentQuestion.question}}
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers" :key="index"
          @click.prevent="selectAnswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
          >
          {{answer}}
        </b-list-group-item>
      </b-list-group>
      <!-- <p v-for="(answer, index) in answers" :key="index">{{answer}}</p> -->

      <b-button  variant="primary" href="#">Submit Answer</b-button>
      <b-button @click="next" variant="success" href="#">Next Question</b-button>
    </b-jumbotron>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  data(){
    return {
      selectedIndex: null,
      shuffledAnswers: []
    }
  },
  props: {
    currentQuestion: Object,
    next: Function,
  },
  methods: {
    selectAnswer: function(index){
      this.selectedIndex = index
    },
    shuffleAnswers: function(){
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers = _.shuffle(answers)
      return this.shuffledAnswers
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler(){
        this.selectedIndex = null
        this.shuffleAnswers()
      }
    }
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
.list-group {
  margin-bottom: 15px
}
.btn {
  margin: 5px 5px;
}
.list-group-item:hover {
  cursor: pointer;
  background-color: lightgrey;
}
.selected {
  background-color: lightblue;
}
.correct {
  background-color: lightgreen;
}
.incorrect {
  background-color: red;
}
</style>
