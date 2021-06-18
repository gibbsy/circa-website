<template>
  <div ref="scroll-legal" class="page-wrapper ancillary-page legals">
    <transition name="fade" appear mode="out-in">
      <div
        ref="logo-peel"
        class="circa-logo logo-corner-left"
        aria-label="circa Logo"
        data-scroll
      >
        <nuxt-link to="/">
          <logo />
        </nuxt-link>
      </div>
    </transition>
    <section id="services-wrapper" class="services__container" data-scroll>
      <div
        class="services-texture-bg pull-right"
        data-scroll
        data-scroll-direction="horizontal"
        data-scroll-speed="2"
      >
        <div
          class="inner-texture"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-2"
        ></div>
      </div>

      <div class="services__content">
        <transition name="fade" appear mode="out-in">
          <block-content
            :class-name="'legals__text text-block--full-width'"
            :blocks="pageData.text"
          ></block-content>
        </transition>
      </div>
    </section>

    <app-footer></app-footer>
  </div>
</template>
<script>
import mobile from "is-mobile";
import imageUrlBuilder from "@sanity/image-url";
import sanityClient from "@/sanityClient";
import AppFooter from "~/components/AppFooter.vue";
import Logo from "~/assets/circa_logo_nofill.svg?inline";
const urlBuilder = imageUrlBuilder(sanityClient);
console.log(mobile());
export default {
  components: {
    Logo,
    AppFooter,
  },
  async asyncData({ route, params }) {
    const query = `*[_type == "legalsPage" && slug.current == "${params.slug}"]{_id, slug, text, title}`;
    const pageData = await sanityClient.fetch(query);
    console.log(pageData[0]);
    return { pageData: pageData[0] };
  },
  data() {
    return {};
  },
  mounted() {},

  methods: {
    init() {
      // this.initScroll();
    },
    urlFor(source) {
      return urlBuilder.image(source);
    },
  },
};
</script>
