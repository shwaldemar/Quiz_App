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
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click.prevent="selectAnswer(index)"
          :class="[
            !answered && selectedIndex === index ? 'selected' : answered && correctIndex === index ? 'correct' : answered && correctIndex !== index ? 'incorrect' : ''
          ]"
        >
          {{answer}}
        </b-list-group-item>
      </b-list-group>
      <!-- <p v-for="(answer, index) in answers" :key="index">{{answer}}</p> -->

      <b-button
      variant="primary"
      @click="submitAnswer"
      :disabled="selectedIndex === null || answered">
      Submit Answer
      </b-button>

      <b-button @click="next" variant="success">Next Question</b-button>
    </b-jumbotron>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  data: function() {
    return {
      selectedIndex: null,
      shuffledAnswers: [],
      correctIndex: null,
      answered: false
    }
  },
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  methods: {
    selectAnswer: function(index){
      this.selectedIndex = index
    },
    shuffleAnswers: function(){
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers = _.shuffle(answers)
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    },
    submitAnswer: function(){
      let isCorrect = false

      if(this.selectedIndex === this.correctIndex){
        isCorrect = true
      }
      this.answered = true

      this.increment(isCorrect)
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler(){
        this.selectedIndex = null
        this.shuffleAnswers()
        this.answered = false
      }
    }
  },
  computed: {
    answers(){
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
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
  background-color: #ff726f;
}
</style>
