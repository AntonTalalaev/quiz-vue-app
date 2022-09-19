<template>
  <div class="result">
    <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">{{ results[resultIndex].desc }}</div>
  </div>
</template>

<script>
  export default {
    props: ["results", "totalCorrectAnswers"],
    computed: {
      resultIndex() {
        let index = 0;
        this.results.forEach((result, i) => {
          if (
            result.min <= this.totalCorrectAnswers &&
            result.max >= this.totalCorrectAnswers
          ) {
            index = i;
            return index;
          }
        });
        return index;
      },
    },
  };
</script>
