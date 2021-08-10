<template>
  <div class="content">
    <Title />
    <Board />
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.content {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
  background: var(--bg-color);
  color: var(--white-color);
}
</style>
