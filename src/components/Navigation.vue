<script>
import "../assets/app.scss";
import IconMenu from "./icons/IconMenu.vue";
export default {
  name: "SlideNavigation",
  methods: {
    toggleSlidePanel() {
      const slidePanel = document.querySelector("div.nav-slide-panel");
      slidePanel.classList.toggle("open");
    },
  },
  components: { IconMenu },
};
</script>

<template>
  <nav class="slide-in-nav">
    <div class="nav-bar">
      <button @click.prevent="toggleSlidePanel">
        <IconMenu />
      </button>
    </div>

    <div class="nav-slide-panel"></div>
  </nav>
</template>

<style lang="scss">
@import "../assets/partials/colours.scss";

nav.slide-in-nav {
  position: fixed;
  z-index: 50;
  top: 0;
  left: 0;
  right: 0;
  width: 100vw;

  .nav-bar {
    width: 100%;
    background-color: $darkBg;
    padding: 1.25rem;
    border-radius: 0 0 0.5rem 0.5rem;
  }

  .nav-slide-panel {
    position: absolute;
    right: 0;
    bottom: 1.25rem;
    max-width: 20rem;
  }
}
</style>
