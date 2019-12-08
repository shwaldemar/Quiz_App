<template>
  <div id="app">

  <Header/>
  <b-container class="bv-example-row">
  <b-row>
    <b-col sm="6" offset="3">
      <QuestionBox
      :currentQuestion="quiz[index]"
      />
    </b-col>
  </b-row>
</b-container>

  </div>
</template>

<script>
import Header from './components/Header';
import QuestionBox from './components/QuestionBox';

export default {
  name: 'app',
  data(){
    return {
      quiz: [],
      index: 0
    }
  },
  components: {
    Header,
    QuestionBox
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&type=multiple')
      .then((response) => {
      return response.json();
    })
      .then((jsonData) => {
        this.quiz = jsonData.results
      })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
