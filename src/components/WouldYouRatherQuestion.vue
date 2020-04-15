<template>
    <div class="would-you-rather-question">
        <!-- List item for each question component -->
        <li>
            <h3>{{question.question}}</h3>
            <!-- v-model to choice variable, send that data and the question's id back to parent on a change -->
             <input type="radio" value="answer1" v-model="choice" v-on:change="$emit('answer-changed', choice, question.id)">
            <label>{{question.answer1}}</label>
            <input type="radio" value="answer2" v-model="choice" v-on:change="$emit('answer-changed', choice, question.id)">
            <label>{{question.answer2}}</label>
        </li>
    </div>
</template>

<script>
export default {
    name: 'WouldYouRatherQuestion',
    data() {
        return {
            choice: ''
        }
    },
    props: {
        question: Object,
    },
}
</script>

<style>
.would-you-rather-question {
    margin-top: 15px;
    border-style: solid;
    border-width: medium;
    border-color: navy;
}
</style>