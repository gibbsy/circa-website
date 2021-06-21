<template>
  <div class="nav__links-wrapper">
    <ul class="nav__links--desktop">
      <li
        @click.prevent="
          scrollTo('#about-wrapper', {
            offset: 2,
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
        <a>What we do</a>
      </li>
      <li
        @click.prevent="
          scrollTo('#work-wrapper', {
            offset: 0,
            duration: 1000,
          })
        "
      >
        <a>Case studies</a>
      </li>
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
    <ul class="nav__links--mobile">
      <li
        @click.prevent="
          scrollTo('#intro-wrapper', {
            offset: 0,
            duration: 1000,
          })
        "
      >
        <a>About</a>
      </li>
      <li
        @click.prevent="
          scrollTo('#work-wrapper', {
            offset: 0,
            duration: 1000,
          })
        "
      >
        <a>Work</a>
      </li>
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
export default {
  props: {
    scroll: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    scrollTo(target, options) {
      this.scroll.scrollTo(target, options);
    },
  },
};
</script>
