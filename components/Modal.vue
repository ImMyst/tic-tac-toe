<template>
  <transition name="modal">
    <div v-if="isOpen" class="modal">
      <div class="modal-content">
        <span class="modal-content-title">
          <slot />
        </span>
        <Button @click="$emit('close:modal')"> Fermer </Button>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    isOpen: {
      type: Boolean,
      default: false,
    },
  },
}
</script>

<style lang="scss" scoped>
.modal {
  position: fixed;
  z-index: 99;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  transition: opacity 0.3s ease;
  &-content {
    min-width: 18rem;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 2rem;
    margin: auto;
    padding: 1.75rem;
    background: var(--bg-color);
    border-radius: 0.4rem;
    transition: all 0.3s ease;
    &-title {
      font-size: 1.25rem;
      text-align: left;
      font-weight: 700;
    }
  }
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>