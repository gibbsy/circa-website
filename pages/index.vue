<template>
  <div id="page-wrapper" ref="scroll" class="home page-wrapper">
    <!--  <div
      class="hero__background"
      data-scroll
      data-scroll-repeat="true"
      data-scroll-sticky="true"
      data-scroll-target="#hero"
      data-scroll-speed="-10"
    >
      <ContentVideo
        player-id="textures"
        vimeo-id="560926320"
        :autoplay="true"
        :wallpaper="true"
        :scroll="scroll"
      ></ContentVideo>
    </div> -->
    <section
      id="hero"
      class="hero__container"
      data-scroll
      data-scroll-call="hero"
      data-scroll-repeat="true"
    >
      <div id="hero-target-50" class="target"></div>
      <div id="hero-target-100" class="target"></div>
      <div id="hero-target-150" class="target"></div>
      <scroll-images
        :animal-images="assets.animalImages"
        :img-res="imgRes"
      ></scroll-images>
      <div
        class="circa-logo logo-corner-left"
        aria-label="circa Logo"
        data-scroll
        data-scroll-sticky="true"
        data-scroll-target="#hero"
      >
        <nuxt-link to="/">
          <logo />
        </nuxt-link>
      </div>
      <transition appear name="fade">
        <nav-desktop ref="nav" :scroll="scroll" />
      </transition>
      <article id="hero-text" class="hero__content" data-scroll data-splitting>
        <div class="hero__title" data-scroll data-scroll-speed="0.2">
          <block-content
            :blocks="hero.heroTitle"
            :serializers="serializers"
          ></block-content>
        </div>
        <div
          class="hero__intro"
          data-scroll
          data-scroll-speed="-1.5"
          data-scroll-offset="100"
        >
          <block-content :blocks="hero.heroBody"></block-content>
        </div>
      </article>
    </section>
    <section class="about__container">
      <div class="about__content">
        <div class="about__title" data-scroll data-splitting>
          <block-content
            :blocks="about.aboutTitle"
            :serializers="serializers"
          ></block-content>
        </div>
        <div class="about__images">
          <div
            v-for="img in about.aboutImages"
            :key="img.title"
            class="about__img"
            :style="{
              backgroundImage: `url('${urlFor(img.asset)
                .width(500)
                .height(500)
                .format('jpg')
                .quality(70)
                .url()}')`,
            }"
          ></div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
// import NavDesktop from "../components/NavDesktop.vue";
// import mobile from "is-mobile";
import imageUrlBuilder from "@sanity/image-url";
import sanityClient from "../sanityClient";
import Logo from "~/assets/circa_logo_nofill.svg?inline";
import copyline from "~/components/span.vue";

const urlBuilder = imageUrlBuilder(sanityClient);

if (typeof window === "undefined") {
  global.window = {};
}
const winSize = {
  width: window.innerWidth,
  height: window.innerHeight,
  dpr: window.devicePixelRatio,
};
const query = `{
  "config": *[_type=="siteConfig"]{"title": siteTitle, "description": siteDescription},
  "assets": *[_type=="brandAssets"]{ animalImages },
	"home": *[_type=="home"][0] {
    "hero": {
      heroTitle, heroBody, heroPrompt
    },
    "about": {
      aboutTitle, aboutBody, aboutStats, aboutImages[] {
          asset->
      }
    },
    "services": {
      servicesTitle, servicesBody, servicesList
    },
    "clients": {
      clientsTitle, clientsIntro, clients
    },
    caseStudies,
    "connect": {
      connectTitle, connectIntro, contactDetails
    }
},
"legals": *[_type == "legalsPage" ]{ title, "slug": slug.current }
}`;
export default {
  components: {
    Logo,
  },
  async asyncData() {
    const homeData = await sanityClient.fetch(query);
    return {
      ...homeData.home,
      assets: homeData.assets[0],
      legals: homeData.legals,
      config: homeData.config[0],
    };
  },
  data() {
    return {
      navActive: false,
      resizeTimeout: 0,
      scroll: {},

      serializers: {
        marks: {
          span: copyline,
        },
      },
    };
  },
  head() {
    const { title, description } = this.config;
    return {
      title,
      meta: [
        {
          hid: "description",
          name: "description",
          content: description,
        },
      ],
    };
  },
  computed: {
    imgRes() {
      const { width, height, dpr } = winSize;
      const imgRes = { dpr: dpr === 3 ? 2 : 1 };
      if (width > 1440) {
        imgRes.width = 1920;
        imgRes.height = 1080;
      } else if (width > 1024) {
        imgRes.width = 1440;
        imgRes.height = 900;
      } else if (width >= 768) {
        imgRes.width = 800;
      } else {
        imgRes.width = 400;
      }
      imgRes.height = Math.round(height * 0.8);
      return imgRes;
    },
  },
  mounted() {
    this.splitText();
    this.$nextTick(() => {
      this.init();
    });
    gsap.registerPlugin(ScrollTrigger);
    console.log(this.assets);
  },
  methods: {
    init() {
      this.initScroll();
    },
    urlFor(source) {
      return urlBuilder.image(source);
    },
    initScroll() {
      const el = this.$refs.scroll;
      this.scroll = new this.LocomotiveScroll({
        el,
        smooth: true,
        getDirection: true,
      });
      setTimeout(() => {
        this.updateScroll();
      }, 500);
      this.initScrollEvents();
    },
    initScrollEvents() {
      window.addEventListener("resize", this.handleResize);
      this.scroll.on("scroll", ScrollTrigger.update);
      this.scroll.on("call", (value, way, obj) => {});
    },
    updateScroll() {
      console.log("update scroll");
      this.scroll.update();
    },
    scrollTo(target, options) {
      this.scroll.scrollTo(target, options);
    },
    handleResize() {
      console.log("Resize");
      clearTimeout(this.resizeTimeout);
      this.resizeTimeout = setTimeout(() => {
        this.updateScroll();
      }, 250);
    },
    splitText() {
      Splitting({
        target: "[data-splitting]",
        key: null,
        by: "lines",
      });
    },
  },
};
</script>
