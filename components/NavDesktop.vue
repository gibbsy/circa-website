<template>
  <div id="nav" ref="nav" class="nav intro-ani" role="navigation">
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
