<template>
  <div v-if = "visible" >
    <form v-bind:style="{ display: none }" >
      <label>
        <input placeholder="Your school e-mail"  type="email" v-model="email" class="form-input" />
      </label>
      <br />
      <label>
        <input placeholder="Group number"  v-model="group" class="form-input" />
      </label>
      <br />
      <button @click="submitForm" class="form-button">Start the test</button>
    </form>
  </div>

  <div v-if = !visible class="test-page">
    <div class="gurami">
      {{ ragaca }}

    </div>
    <input v-bind:style="{backgroundColor: color }"  v-for = "a in questions" type="text"  :id=a.question placeholder="Answer here" class="answer-button" :v-model = answer1  @click = showQuestion >
    <p>Exam for group N:{{ group }}</p>
    <p>press the input to check the question</p>
    <button   class="form-button">Submit</button>


  </div>

 
  


</template>

<script>
export default {
  data() {
    return {
      email: null,
      group: null,
      visible: true,
      answer1: null,
      answer2: null,
      answer3: null,
      ragaca: null,
      color: null,
      questions: [
        {id: 1,question: "The side of a square is 5 meters,find area", answer: "25"},
        {id: 2,question: "Which number is larger, -5 or -3", answer: "-3"},
        {id: 3,question: "What is 85% of 21", answer: "17.85"}
      ]
    }
  },
  methods: {
    submit(){
      

    },
    showQuestion(e){
      this.ragaca = e.target.id

    },
    submitForm() {
      if(this.group!=null && this.email!=null){
        this.visible = false
        console.log(this.email)

      }
      else{
        alert("Enter your e-mail and group number")
      }
     
   
    }
  }
}
</script>

<style>
.form-input {
  width: 300px;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 10px;
}
.answer-button{
  width: 300px;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 10px;
  display:block ;

}
.gurami{
  font-size: 14px;
  font-weight: bold;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
.password{
  display: inline;
  margin: -10px;
}

.form-button {
  width: 200px;
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.form-button:hover {
  background-color: #45a049;
}

body{
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #84D2C5;
}
</style>
