<script>

// Api link : https://opentdb.com/api.php?amount=1

export default {
  name: 'App',
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswers: undefined
    }
  },
  computed: {
    answers(){
      var answers = [...this.incorrectAnswers];
      answers.push(this.correctAnswers);
      return answers;
    }
  },
  created(){
    try {
        this.axios.get('https://opentdb.com/api.php?amount=1').then((response) => {
        this.question = response.data.results[0].question;
        this.incorrectAnswers = response.data.results[0]['incorrect_answers'];
        this.correctAnswers = response.data.results[0]['correct_answer'];
        //console.log(response.data.results[0]);
      })
    } catch(err) {

      console.log(err)
      this.question = "no question";
    };
  }
}

</script>

<template>

  <div>
    <h1 v-html="this.question"></h1>

    <input type="radio" name="options" value="True">
    <label>True</label><br>

    <input type="radio" name="options" value="False">
    <label>False</label><br>

    <button class="send" type="button">Send</button>

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
