<script>
import "../assets/app.scss";
import IconMenu from "./icons/IconMenu.vue";

export default {
  name: "SlideNavigation",
  data() {
    return {
      navVisibility: false,
      navItems: [
        {
          name: "Home",
          url: "/",
          aria: "Navigate to homepage",
          active: true,
        },
        {
          name: "About Us",
          url: "/",
          aria: "Navigate to About us",
          active: false,
        },
        {
          name: "Our Projects",
          url: "/",
          aria: "Navigate to Our projects",
          active: false,
        },
        {
          name: "Developer Guides",
          url: "/",
          aria: "Navigate to Developer guides",
          active: false,
        },
        {
          name: "Free Components",
          url: "/",
          aria: "Navigate to Components hub",
          active: true,
        },
        {
          name: "Reccomended Resources",
          url: "/",
          aria: "Navigate to Reccomended resources",
          active: false,
        },
      ],
    };
  },
  methods: {
    toggleSlidePanel() {
      const slidePanel = document.querySelector("div.nav-slide-panel");
      slidePanel.classList.toggle("open");
    },
  },
  computed: {
    navClass: function () {
      return {
        show: this.navVisibility,
      };
    },
  },
  components: { IconMenu },
};
</script>

<template>
  <nav class="slide-in-nav">
    <div class="nav-bar">
      <button class="nav-control" @click="navVisibility = !navVisibility">
        <IconMenu />
      </button>
    </div>

    <div class="nav-slide-panel" v-if="navItems" :class="navClass">
      <a
        v-for="item in navItems"
        :key="item.key"
        :href="item.url"
        class="nav-item"
        :aria-label="item.aria"
      >
        {{ item.name }}
      </a>
    </div>
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
}

.nav-bar,
.nav-slide-panel {
  background-color: $darkBg;
  padding: 1.25rem;
}

.nav-bar {
  width: 100%;
  min-height: 5rem;
  border-radius: 0 0 0.5rem 0.5rem;

  button.nav-control {
    float: right;
  }

  svg.menu-icon {
    width: 2.5rem;
    color: $white;
  }
}

.nav-slide-panel {
  position: absolute;
  right: 0;
  top: 6.25rem;
  max-width: 20rem;
  height: calc(100vh - 6.25rem);
  border-radius: 0.5rem 0 0 0.5rem;
  transform: translateX(100%);
  transition: all;
  transition-duration: 300ms;

  &.show {
    transform: translateX(0);
  }
}
</style>
