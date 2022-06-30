<script>
import "../assets/app.scss";
import IconArrow from "./icons/IconArrow.vue";
import IconInsta from "./icons/IconInsta.vue";
import IconGithub from "./icons/IconGithub.vue";
import SolidButton from "./SolidButton.vue";

export default {
  name: "SlideNavigation",
  data() {
    return {
      navVisibility: false,
      navigation: {
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
        navActions: {
          telephone: {
            name: "07123456789",
            url: "tel:+447123456789",
            aria: "Call us now",
          },
          email: {
            name: "info@email.com",
            url: "mailto:info@email.com",
            aria: "Send us an email",
          },
          callToAction: {
            name: "Get in touch",
            url: "/",
            aria: "Navigate to the contact page",
          },
        },
        navSocialItems: {
          github: {
            url: "https://github.com/LucyRa/slide-in-navigation/blob/main/README.md",
            aria: "Navigate to project GitHub repo",
          },
          instagram: {
            url: "https://www.instagram.com/lramplin/",
            aria: "Navigate to the LRamplin Instagram profile",
          },
        },
      },
    };
  },
  methods: {
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
    navControlClass: function () {
      return {
        active: this.navVisibility,
      };
    },
  },
  components: { IconArrow, IconGithub, IconInsta, SolidButton },
};
</script>

<template>
  <nav class="slide-in-nav">
    <div class="nav-bar">
      <div class="nav-logo"></div>

      <button
        class="nav-control"
        :class="navControlClass"
        @click="navVisibility = !navVisibility"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>

    <div class="nav-slide-panel" v-if="navigation.navItems" :class="navClass">
      <div class="nav-items-container">
        <a
          v-for="item in navigation.navItems"
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

      <div class="nav-actions-container" v-if="navigation.navActions">
        <a
          v-for="(action, name) in navigation.navActions"
          :key="action.key"
          :href="action.url"
          class="nav-action"
          :aria-label="action.aria"
        >
          <SolidButton v-if="name === 'callToAction'" :name="action.name" />

          <span v-else :class="name">
            {{ action.name }}
          </span>
        </a>
      </div>

      <div class="nav-social-container">
        <a
          v-for="(item, name) in navigation.navSocialItems"
          :key="item.key"
          :href="item.url"
          :aria-label="item.aria"
          class="nav-social-item"
        >
          <IconGithub v-if="name === 'github'" />

          <IconInsta v-if="name === 'instagram'" />
        </a>
      </div>
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
  backdrop-filter: blur(0.75rem);
  box-shadow: 0px 2px 20px rgba(84, 82, 88, 0.06);
}

.nav-bar {
  width: 100%;
  min-height: 5rem;
  border-radius: 0 0 0.4rem 0.4rem;
  padding: 1.25rem 2.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;

  svg.menu-icon {
    width: 1.5rem;
    color: $white;
  }
}

button.nav-control {
  position: relative;
  width: 1.666875rem;
  height: 1.25rem;

  span {
    position: absolute;
    display: block;
    width: 1.666875rem;
    height: 1px;
    background-color: $white;
    transition: transform 300ms ease;
    border-radius: 999px;

    &:first-child {
      top: 0;
    }

    &:nth-child(2) {
      top: 50%;
      transition: all 300ms ease;
    }

    &:last-child {
      bottom: 0;
    }
  }

  &.active {
    span {
      &:first-child,
      &:last-child {
        top: 50%;
      }

      &:first-child {
        transform: translateY(-50%) rotate(45deg);
      }

      &:nth-child(2) {
        opacity: 0;
      }

      &:last-child {
        bottom: unset;
        transform: translateY(-50%) rotate(-45deg);
      }
    }
  }
}

.nav-logo {
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 5rem;
  background-color: $brightBlue;
}

.nav-slide-panel {
  position: absolute;
  right: 0;
  top: 4.5rem;
  width: 100%;
  height: calc(100vh - 4.5rem);
  transform: translateY(100%);
  transition: transform 300ms linear;
  will-change: transform;
  padding: 2.5rem 1.25rem;
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: space-between;
  overflow: scroll;

  &.show {
    transform: translateY(0);
    transition: transform 300ms linear;
  }
}

.nav-items-container,
.nav-actions-container,
.nav-social-container {
  width: 100%;
}

.nav-items-container {
  margin-bottom: 2.5rem;
}

a.nav-item {
  display: block;
  position: relative;
  width: fit-content;
  margin-bottom: 1.25rem;
  font-size: 1.125rem;
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

.nav-actions-container {
  padding-top: 1.875rem;
  border-top: 1px solid $white;
}

a.nav-action {
  width: 100%;
  margin-bottom: 1.25rem;

  button.btn-solid {
    width: 100%;
    margin-top: 1.875rem;
  }

  span {
    position: relative;
    display: block;
    padding-left: 2.125rem;
    color: $grey;
    transition: color 300ms ease;

    &::before {
      content: "";
      display: block;
      width: 1.375rem;
      height: 1.375rem;
      background-size: 1.375rem 1.375rem;
      background-repeat: no-repeat;
      position: absolute;
      left: 0;
    }

    &.telephone {
      &::before {
        background-image: url("../assets/phone.svg");
      }
    }

    &.email {
      &::before {
        background-image: url("../assets/mail.svg");
      }
    }

    &:hover {
      color: $white;
    }
  }

  &:last-child {
    margin-bottom: 0;
  }
}

.nav-social-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.25rem;
  flex-wrap: wrap;
  margin-top: 1.25rem;
}

a.nav-social-item {
  width: 2.5rem;

  svg {
    width: 2.5rem;
  }
}

@media only screen and (min-width: 480px) {
  .nav-slide-panel {
    max-width: 20rem;
    border-radius: 0.4rem 0 0 0;
    transform: translateX(100%);
    height: calc(100vh - 6.25rem);
    top: 6.25rem;

    &.show {
      transform: translateX(0);
    }
  }
}

@media only screen and (min-width: 768px) {
  .nav-items-container {
    margin-bottom: 3.75rem;
  }

  .nav-slide-panel {
    padding: 2.75rem 2rem;
  }

  a.nav-item {
    margin-bottom: 1.5rem;
  }

  .nav-actions-container {
    padding-top: 2.5rem;
  }

  a.nav-action {
    button.btn-solid {
      margin-top: 2.5rem;
    }
  }
}
</style>
