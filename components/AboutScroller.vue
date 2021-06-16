<template>
  <div class="about__scroller-wrapper" data-scroll data-scroll-offset="35%">
    <div id="about-images-container" class="about__images">
      <div v-for="img in about.aboutImages" :key="img.title" class="about__img">
        <figure
          class="inner-image"
          :style="{
            backgroundImage: `url('${urlFor(img.asset)
              .width(500)
              .height(500)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></figure>
      </div>
    </div>
    <div id="about-stats-container" class="about__stats">
      <div v-for="(stat, i) in about.aboutStats" :key="i" class="stat-wrapper">
        <h2 class="stat">{{ stat.stat }}</h2>
        <div class="stat__text">
          <h3>{{ stat.title }}</h3>
          <p>{{ stat.text }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import imageUrlBuilder from "@sanity/image-url";
import sanityClient from "../sanityClient";
import copyline from "~/components/span.vue";

const urlBuilder = imageUrlBuilder(sanityClient);
export default {
  props: {
    about: {
      type: Object,
      default: () => {},
    },
    scroll: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      serializers: {
        marks: {
          span: copyline,
        },
      },
    };
  },
  mounted() {
    /*  this.$nextTick(() => {
      this.initScrollAni();
    }); */
    const imgLoad = imagesLoaded(
      "#about-images-container",
      { background: true },
      () => {
        const that = this;
        this.initScrollAni();
        setTimeout(() => {
          that.updateScroll();
        }, 500);
      }
    );
    imgLoad.on("progress", function (instance, image) {
      const result = image.isLoaded ? "loaded" : "broken";
      console.log("image is " + result + " for " + image.img.src);
    });
  },
  methods: {
    initScrollAni() {
      const scrollContainer = document.getElementById("page-wrapper");
      const images = document.getElementById("about-images-container");
      const stats = document.getElementById("about-stats-container");

      const tl = gsap.timeline({
        scrollTrigger: {
          scroller: scrollContainer,
          trigger: "#about-wrapper",
          start: "top top",
          scrub: true,
          pin: true,
          end: "+=200%",
        },
      });
      tl.to(
        images,
        {
          x: "-=100%",
          duration: 4,
          ease: "sine.inOut",
        },
        0
      );
      tl.to(
        stats,
        {
          x: "-=100%",
          duration: 4,
          ease: "sine.inOut",
        },
        0
      );
      this.$nextTick(() => {
        this.updateScroll();
      });
    },
    urlFor(source) {
      return urlBuilder.image(source);
    },
    updateScroll() {
      console.log("update scroll");
      this.scroll.update();
      ScrollTrigger.refresh();
    },
  },
};
</script>
