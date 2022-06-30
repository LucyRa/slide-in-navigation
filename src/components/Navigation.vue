<script>
import "../assets/app.scss";
import IconMenu from "./icons/IconMenu.vue";
import IconArrow from "./icons/IconArrow.vue";

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
          active: false,
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
    activeNavItem: (active) => {
      return {
        active: active,
      };
    },
  },
  computed: {
    navClass: function () {
      return {
        show: this.navVisibility,
      };
    },
  },
  components: { IconMenu, IconArrow },
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
        :class="activeNavItem(item.active)"
        :aria-label="item.aria"
      >
        {{ item.name }}

        <IconArrow v-if="item.active == false" />
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
  backdrop-filter: blur(0.75rem);
  box-shadow: 0px 2px 20px rgba(84, 82, 88, 0.06);
}

.nav-bar {
  width: 100%;
  min-height: 3.875rem;
  border-radius: 0 0 0.5rem 0.5rem;

  button.nav-control {
    float: right;
  }

  svg.menu-icon {
    width: 1.5rem;
    color: $white;
  }
}

.nav-slide-panel {
  position: absolute;
  right: 0;
  top: 5.125rem;
  width: 100%;
  max-width: 20rem;
  height: calc(100vh - 5.125rem);
  border-radius: 0.5rem 0 0 0;
  transform: translateX(100%);
  transition: all;
  transition-duration: 400ms;
  padding: 3.75rem 2.5rem;

  &.show {
    transform: translateX(0);
  }
}

a.nav-item {
  display: block;
  position: relative;
  width: fit-content;
  margin-bottom: 1.5rem;
  color: #ffffff;
  transition: all 300ms ease-in-out;

  svg.arrow-icon {
    width: 1.125rem;
    color: $brightBlue;
    margin-left: 0.5rem;
  }

  &.active {
    color: $lightGreen;
  }

  &:last-child {
    margin-bottom: 0;
  }

  &:hover {
    transform: scale(1.06);
  }
}
</style>
