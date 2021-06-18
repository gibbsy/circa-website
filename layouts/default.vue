<template>
  <div>
    <div :id="containerId" data-scroll-container>
      <Nuxt />
    </div>
  </div>
</template>
<script>
export default {
  computed: {
    containerId() {
      return this.$route.name;
    },
  },
  watch: {
    $route(value) {
      this.page = value.name;
      console.log(value);
    },
  },
};
</script>
