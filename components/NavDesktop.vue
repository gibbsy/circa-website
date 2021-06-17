<template>
  <div id="nav" ref="nav" class="nav intro-ani" role="navigation">
    <nav-links :scroll="scroll" />
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
