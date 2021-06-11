<template>
  <div class="about__scroller-wrapper">
    <div id="about-images-container" class="about__images">
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
    <div id="about-stats-container" class="about__stats">
      <div v-for="(stat, i) in about.aboutStats" :key="i" class="stat">
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
    this.initScrollAni();
  },
  methods: {
    initScrollAni() {
      const scrollContainer = document.getElementById("page-wrapper");
      const images = document.getElementById("about-images-container");
      const stats = document.getElementById("about-stats-container");
      const scrollerWidth = images.offsetWidth;
      const scrollLength = scrollerWidth - window.innerWidth;
      console.log(scrollerWidth, scrollLength);

      const tl = gsap.timeline({
        scrollTrigger: {
          scroller: scrollContainer,
          trigger: "#about-wrapper",
          start: "top top",
          scrub: true,
          // markers: true,
          pin: true,
          end: "+=100%",
        },
      });
      tl.to(
        images,
        {
          // x: `-=${scrollLength}`,
          x: "-=100%",
          duration: 4,
          ease: "sine.inOut",
        },
        0
      );
      tl.to(
        stats,
        {
          // x: `-=${scrollLength}`,
          x: "-=100%",
          duration: 4,
          ease: "sine.inOut",
        },
        0
      );
      this.updateScroll();
      ScrollTrigger.refresh();

      /*    const pinBoxes = document.querySelectorAll(".pin-wrap > *");
      const pinWrap = document.querySelector(".pin-wrap");
      const pinWrapWidth = pinWrap.offsetWidth;
      const horizontalScrollLength = pinWrapWidth - window.innerWidth;

      // Pinning and horizontal scrolling

      gsap.to(".pin-wrap", {
        scrollTrigger: {
          scroller: pageContainer, // locomotive-scroll
          scrub: true,
          trigger: "#sectionPin",
          pin: true,
          // anticipatePin: 1,
          start: "top top",
          end: pinWrapWidth,
        },
        x: -horizontalScrollLength,
        ease: "none",
      }); */
    },
    urlFor(source) {
      return urlBuilder.image(source);
    },
    updateScroll() {
      console.log("update scroll");
      this.scroll.update();
    },
  },
};
</script>
