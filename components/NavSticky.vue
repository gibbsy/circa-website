<template>
  <div :class="[{ active }, 'nav__sticky-wrapper']">
    <div id="nav-sticky" :class="[{ dark }, 'nav__sticky']" role="navigation">
      <div class="circa-logo" aria-label="circa Logo">
        <a
          aria-label="Scroll to top"
          href
          @click.prevent="
            scrollTo('#hero', {
              offset: 0,
              duration: 1000,
            })
          "
        >
          <logo
        /></a>
      </div>
      <ul class="nav__links-desktop">
        <li
          @click.prevent="
            scrollTo('#about-wrapper', {
              offset: 0,
              duration: 1000,
            })
          "
        >
          <a>Story</a>
        </li>
        <li
          @click.prevent="
            scrollTo('#services-wrapper', {
              offset: 0,
              duration: 1000,
            })
          "
        >
          <a>Services</a>
        </li>
        <li
          @click.prevent="
            scrollTo('#clients-wrapper', {
              offset: 0,
              duration: 1000,
            })
          "
        >
          <a>Clients</a>
        </li>
        <!-- <li
        @click.prevent="
          scrollTo('#work-wrapper', {
            offset: 0,
            duration: 1000,
          })
        "
      >
        <a>Work</a>
      </li> -->
        <li
          @click.prevent="
            scrollTo('#connect-wrapper', {
              offset: 0,
              duration: 1000,
            })
          "
        >
          <a>Connect</a>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import mobile from "is-mobile";
import Logo from "~/assets/circa_logo_nofill.svg?inline";
export default {
  components: {
    Logo,
  },
  props: {
    active: {
      type: Boolean,
      default: false,
    },
    dark: {
      type: Boolean,
      default: false,
    },
    scroll: {
      type: Object,
      default: () => {},
    },
  },
  /*  data() {
    return {
      showProducts: false,
    };
  }, */
  computed: {
    isMobile() {
      return mobile();
    },
  },
  methods: {
    scrollTo(target, options) {
      this.scroll.scrollTo(target, options);
    },
  },
};
</script>
