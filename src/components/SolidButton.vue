<script>
export default {
  name: "SolidButton",
  props: ["name"],
};
</script>

<template>
  <button v-if="name" class="btn-solid">
    {{ name }}
  </button>
</template>

<style lang="scss">
@import "../assets/partials/colours.scss";

button.btn-solid {
  width: fit-content;
  padding: 0.53125rem 1rem;
  border-radius: 0.5rem;
  background-color: $brightBlue;
  color: $dark;
  font-weight: 500;
  transition: all 300ms ease-in-out;

  &:hover {
    background-color: $white;
  }
}
</style>
