<template>
  <ul class="nav__links-desktop">
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
    <!--       <li
        @click.prevent="
          scrollTo('#clients-wrapper', {
            offset: 0,
            duration: 1000,
          })
        "
      >
        <a>Clients</a>
      </li> -->
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
