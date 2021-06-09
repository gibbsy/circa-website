<template>
  <div id="nav" ref="nav" class="nav intro-ani" role="navigation">
    <ul class="nav__links-desktop">
      <li>
        <a>About</a>
      </li>
      <li
        @click.prevent="
          scrollTo('#feature-2', {
            offset: 0,
            duration: 1000,
          })
        "
      >
        <a>Work</a>
      </li>
      <li
        @click.prevent="
          scrollTo('#feature-2', {
            offset: 0,
            duration: 1000,
          })
        "
      >
        <a>Contact</a>
      </li>
    </ul>
  </div>
</template>
<script>
import mobile from "is-mobile";
export default {
  props: {
    scroll: {
      type: Object,
      default: () => {},
    },
  },
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
