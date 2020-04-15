<template>
  <div id="app">
    <h1>Would you rather ... </h1>
      <div> 
        <!-- WYRQ instance -->
        <!-- Loop for each question-->
        <!-- answerChanged method when answer is changed -->
          <WouldYouRatherQuestion 
          v-for="question in questions"
          v-bind:key="question.id"
          v-bind:question="question"
          v-on:answer-changed="answerChanged"
          ></WouldYouRatherQuestion>  
      </div>

      <div>
        <h1>You would rather ... </h1>
        <!-- If no questions are answered, don't display answers -->
        <h3 v-if="answeredQuestions.length < 1">Fill in some answers</h3>
        <!-- Otherwise a list item for each answered question -->
        <ul v-else>
          <li
           v-for="answeredQuestion in answeredQuestions"
          v-bind:key="answeredQuestion"
          >{{answeredQuestion}}
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
import WouldYouRatherQuestion from './components/WouldYouRatherQuestion.vue'

export default {
  name: 'App',
  components: {
    WouldYouRatherQuestion
  },
  data() {
    return {
      questions: [
        {
          id: 0,
          question: 'eat cake or hot dogs?',
          answer1: 'eat cake',
          answer2: 'eat hot dogs'
        },
        {
          id: 1,
          question: 'watch tv or read a book?',
          answer1: 'watch tv',
          answer2: 'read a book'
        },
        {
          id: 2,
          question: 'wear a sweater or a tee shirt?',
          answer1: 'wear a sweater',
          answer2: 'wear a tee shirt'
        }
      ],
      // Blank array and strings to be filled with answers below
      answeredQuestions : [],
      chosenAnswer : '',
      otherAnswer : ''
    }
  },
  methods: {
    answerChanged(choice, id) {
      // Test which answer is coming in and assign variables accordingly
      if(choice === 'answer1') {
        // Choice comes in formatted to match the keys for the answers in a question object
        this.chosenAnswer = this.questions[id].answer1
        this.otherAnswer = this.questions[id].answer2
      } else {
        this.chosenAnswer = this.questions[id].answer2
        this.otherAnswer = this.questions[id].answer1
      } 

      // Test if we have an answer to every question and if the questions other answer is already in the array
      if(this.answeredQuestions.length < this.questions.length && !this.answeredQuestions.includes(this.otherAnswer)) {
        // just plain add the answer
        this.answeredQuestions.push(this.chosenAnswer)
      } else {
        // Otherwise, must remove the counterpart answer and replace with currently selected answer
        this.answeredQuestions.splice(id, 1, this.chosenAnswer)
      }

      // Reset variables
      this.chosenAnswer = ''
      this.otherAnswer = ''

    }
  }
}
</script>

<style>
#app {
}
</style>
