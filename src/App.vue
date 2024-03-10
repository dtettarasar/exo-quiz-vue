<script>

// Api link : https://opentdb.com/api.php?amount=1

export default {
  name: 'App',
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswers: undefined,
      chosenAnswer: undefined
    }
  },
  computed: {
    answers(){
      var answers = [...this.incorrectAnswers];
      let randomInd = this.getRandomInd();
      answers.splice(randomInd, 0, this.correctAnswers);
      return answers;
    }
  },
  created(){
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
  },
  methods: {

    getRandomInd (){
      // get a random index to insert the correct answer in the computed answer data
      const index = Math.round(Math.random() * this.incorrectAnswers.length);
      return index;

    },

    submitForm () {

      if (this.chosenAnswer === undefined) {
        
        alert('pick an answer');

      } else if (this.correctAnswers === this.chosenAnswer) {

        alert('good answer');

      } else {

        alert('wrong answer');

      }

    }

  }
}

</script>

<template>

  <div>

    <template v-if="this.question">
      
      <h1 v-html="this.question"></h1>
  
      <template v-for="(answer, index) in this.answers" :key="index">
  
        <input type="radio" name="options" :value="answer" v-model="chosenAnswer">
        <label v-html="answer" ></label>
        <br>
  
      </template>

      <button v-on:click="this.submitForm()" class="send" type="button">Send</button>

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
