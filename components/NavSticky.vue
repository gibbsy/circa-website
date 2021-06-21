<template>
  <div :class="[{ active }, 'nav__sticky-wrapper']">
    <div id="nav-sticky" :class="[{ dark }, 'nav__sticky']" role="navigation">
      <div class="circa-logo" aria-label="circa Logo">
        <a
          aria-label="Scroll to top"
          href
          @click.prevent="
            scrollTo('#hero-container', {
              offset: 0,
              duration: 1000,
            })
          "
        >
          <logo
        /></a>
      </div>
      <nav-links :scroll="scroll" />
    </div>
  </div>
</template>
<script>
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
  methods: {
    scrollTo(target, options) {
      this.scroll.scrollTo(target, options);
    },
  },
};
</script>
