<template>
  <div id="app">
    <div id="todoApp">
      <div>
        <div 
            v-for="(question, questionIndex) in questions"
            :key="questionIndex"
            v-show="current == questionIndex">
            <div>{{ question.content }}</div>
            <div 
              v-for="(ans, ansIndex) in question.answers"
              :key="ansIndex"
              @click="question.selected = ansIndex"
              :class="{selected: question.selected == ansIndex}">
            {{ ans }}</div>
            <div>
          <button @click="current--" v-show="current >= 0 && current < questions.length" :disabled="current == 0">Pre</button>
          <button @click="current++" v-show="current < questions.length - 1" :disabled="question.selected == null">Next</button>
          <button @click="current++" v-show="current == questions.length - 1" :disabled="question.selected == null">Finish</button>
        </div>
        </div>
        
      </div>
      <div v-show="current == questions.length">
        Ket qua: {{ questions.filter (question => question.correct == question.selected ).length }} / {{ questions.length }}
        <div><button @click="current = 0; questions.forEach( question => question.selected = null )">Reset</button></div>
      </div>
    </div>
  </div>

</template>

<script>
export default {
      
        data() {
            return {
              current: 0,
              questions: [
                {
                   content: '1 + 1 = ?',
                   answers: [1,2,3,4],
                   correct: 1,
                   selected: null,
                }, 
                {
                   content: '1 + 3 = ?',
                   answers: [1,2,3,4],
                   correct: 3,
                   selected: null,
                }, 
                {
                   content: "What is the best cookie?",
                   answers: [
                     "Chocolate Chip",
                     "Sugar",
                     "Beer",
                     "Oreo"
                   ],
                   correct: 3,
                   selected: null,
                }
              ]
            }
        }
    }

</script>


<style>
#todoApp{
  max-width: 400px;
  border: 1px solid #ebebeb;
  margin: 10px auto;
  padding: 10px;

}
.selected {
  border: 1px solid red;
}
</style>
