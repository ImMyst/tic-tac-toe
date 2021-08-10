<template>
  <div class="case" @click="onClick">
    <span :class="`case-value case-value-${value}`">
      {{ value }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: null,
    },
  },
  methods: {
    onClick() {
      this.$emit('case:clicked')
    },
  },
}
</script>

<style lang="scss" scoped>
.case {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 4.5rem;
  width: 4.5rem;
  margin: 0.35rem 0.175rem;
  border-radius: 0.4rem;
  cursor: pointer;
  background: var(--case-bg-color);
  &-value {
    color: var(--case-bg-color);
    font-size: 3.5rem;
    transition: all 0.3s;
  }
  &-value-X {
    color: var(--primary-color);
  }
  &-value-O {
    color: var(--accent-color);
  }
}
</style>