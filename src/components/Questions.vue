<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        :style="{
          width: `${(questionsAnswered / questions.length) * 100}%`,
        }"
        class="bar"
      ></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div
        v-show="questionsAnswered === qi"
        v-for="(question, qi) in questions"
        :key="question.q"
        class="single-question"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            v-for="answer in question.answers"
            :key="answer.text"
            @click.prevent="selectAnswer(answer.is_correct)"
            class="answer"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
  export default {
    props: ["questions", "questionsAnswered"],
    emits: ["question-answered"],
    methods: {
      selectAnswer(isCorrect) {
        this.$emit("question-answered", isCorrect);
      },
    },
  };
</script>
