<template>
  <div class="score">
    <span class="score-x">{{ xScore }}</span>
    <span>VS</span>
    <span class="score-o">{{ oScore }}</span>
  </div>
</template>

<script>
export default {
  props: {
    xScore: {
      type: Number,
      required: true,
    },
    oScore: {
      type: Number,
      required: true,
    },
  },
}
</script>

<style lang="scss" scoped>
.score {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
  font-size: 1.4rem;
  font-weight: 700;
  &-x {
    color: var(--primary-color);
  }
  &-o {
    color: var(--accent-color);
  }
}
</style>