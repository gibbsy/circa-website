<template>
  <div>
    <div :id="containerId" data-scroll-container>
      <Nuxt />
      <transition name="fade" appear>
        <cookie-panel
          v-show="!cookiesOk"
          :click-fn="acceptCookies"
        ></cookie-panel>
      </transition>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      cookiesOk: true,
    };
  },
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
  mounted() {
    window.setTimeout(() => {
      this.cookiesOk = this.$cookies.get("circa-accept-cookies");
      // this.cookiesOk = false;
    }, 3000);
  },
  methods: {
    acceptCookies() {
      console.log("cookies Ok");
      this.cookiesOk = true;
      this.$cookies.set("circa-accept-cookies", "true", {
        path: "/",
        maxAge: 60 * 60 * 24 * 90,
      });
    },
  },
};
</script>
