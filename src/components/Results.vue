<template>
  <p>Reaction time - {{ score }} ms</p>
  <p class="rank">{{ rank }}</p>
</template>

<script>
export default {
  props: ["score"],
  data() {
    return {
      rank: null,
    };
  },
  mounted() {
    if (this.score < 200) {
      this.rank = "Extremely Fast";
    } else if (this.score < 300) {
      this.rank = "Fast";
    } else if (this.score < 500) {
      this.rank = "Moderate";
    } else if (this.score < 600) {
      this.rank = "Slow";
    } else {
      this.rank = "Extremely Slow";
    }
  },
};
</script>

<style>
.rank {
  font-size: 1rem;
  color: #0faf87;
  font-weight: bold;
}
</style>
