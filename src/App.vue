<script>

// Api link : https://opentdb.com/api.php?amount=1

import ScoreBoard from './components/ScoreBoard.vue'

export default {

  name: 'App',
  components: {
    ScoreBoard
  },
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswers: undefined,
      chosenAnswer: undefined,
      answerSubmitted: false,
      playerScore: 0,
      cpuScore: 0
    }
  },
  computed: {
    answers(){
      var answers = [...this.incorrectAnswers];
      let randomInd = this.getRandomInd();
      answers.splice(randomInd, 0, this.correctAnswers);
      return answers;
    },
    userGotRightAnswer() {
      return this.chosenAnswer === this.correctAnswers;
    }
  },
  created(){
    this.getNewQuestion();
  },
  methods: {

    getRandomInd (){
      // get a random index to insert the correct answer in the computed answer data
      const index = Math.round(Math.random() * this.incorrectAnswers.length);
      return index;

    },

    submitForm () {

      if (this.chosenAnswer === undefined) {

        console.log("pick an answer");

      } else {

        this.answerSubmitted = this.chosenAnswer;

        if (this.chosenAnswer === this.correctAnswers) {

          console.log("good answer");
          this.playerScore++;

        } else {

          console.log("wrong answer");
          this.cpuScore++;

        }

      }

    },

    getNewQuestion () {
      try {
        this.axios.get('https://opentdb.com/api.php?amount=1').then((response) => {
        this.question = response.data.results[0].question;
        this.incorrectAnswers = response.data.results[0]['incorrect_answers'];
        this.correctAnswers = response.data.results[0]['correct_answer'];
      })
      } catch(err) {

        console.log(err)
        this.question = "no question";

      };

      this.chosenAnswer = undefined;
      this.answerSubmitted = false;
      this.question = undefined;

    }


  }
}

</script>

<template>

  <div>

    <ScoreBoard />

    <template v-if="this.question">
      
      <h1 v-html="this.question"></h1>
  
      <template v-for="(answer, index) in this.answers" :key="index">
  
        <input :disabled="this.answerSubmitted" type="radio" name="options" :value="answer" v-model="chosenAnswer">
        <label v-html="answer" ></label>
        <br>
  
      </template>

      <section v-if="this.answerSubmitted" class="result" >
        <h4 v-html="'Well done, &quot;' + this.correctAnswers + '&quot; is the right answer.'" v-if="this.userGotRightAnswer"></h4>
        <h4 v-html="'Sorry but nope! &quot;' + this.correctAnswers + '&quot; is the right answer'" v-else></h4>
        <button @click="this.getNewQuestion()" class="send" type="button">Next Question</button>
      </section>

      <button v-if="!this.answerSubmitted" v-on:click="this.submitForm()" class="send" type="button">Send</button>

    </template>



  </div>
  
</template>

<style scoped>

  #app input[type=radio] {
    margin: 12px 4px;
  }

  #app button.send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #fff;
    background-color: #ce181e;
    border: 1px solid #ce181e;
    cursor:pointer
  }

</style>
