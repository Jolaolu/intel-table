<template>
  <transition name="toast">
    <div :class="['toast', context]">{{ message }}</div>
  </transition>
</template>

<script>
export default {
  name: "Toast",
  props: ["message", "context"]
};
</script>
<style lang="scss" scoped>
.toast {
  display: flex;
  position: fixed;
  justify-content: center;
  width: 50%;
  padding: 1.5rem 2rem;
  border-radius: 5px;
  cursor: pointer;
  color: white;
  font-size: 1.2em;
  font-weight: 500;
  text-align: left;
  &.error {
    background-color: #ef5753;
  }
  &.success {
    background-color: #51d88a;
  }
}
.toast-enter,
.toast-leave-to {
  opacity: 0;
  transform: translateY(-100px);
}
.toast-enter-active,
.toast-leave-active {
  transition: all 0.6s;
}
</style>
