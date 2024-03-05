<script>

// Api link : https://opentdb.com/api.php?amount=1

export default {
  name: 'App',
  created(){
    this.axios.get('https://opentdb.com/api.php?amount=1').then((response) => {
      console.log(response.data.results[0]);
    })
  }
}

</script>

<template>

  <div>
    <h1>Quiz Game</h1>

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
