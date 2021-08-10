<template>
  <button class="btn" @click="onClick">
    <slot />
  </button>
</template>

<script>
export default {
  methods: {
    onClick() {
      this.$emit('click')
    },
  },
}
</script>

<style lang="scss" scoped>
.btn {
  display: block;
  text-align: center;
  outline: none;
  border: none;
  border-radius: 0.4rem;
  padding: 0.8rem 0.6rem;
  background-color: var(--primary-color);
  color: var(--white-color);
  cursor: pointer;
  font-size: 1.3rem;
  font-weight: 700;
  transition: opacity 0.2s, transform 0.2s;
  &:hover {
    opacity: 0.9;
  }
  &:active {
    opacity: 0.8;
    transform: scale(0.96);
  }
}
</style>