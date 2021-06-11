<template>
  <div
    class="hero__background"
    data-scroll
    data-scroll-sticky="true"
    data-scroll-target="#hero"
  >
    <div class="hero__images">
      <div class="texture-bg bg-6 pull-left">
        <div class="inner-texture"></div>
        <div class="hero-logo">
          <logo-left />
        </div>
      </div>
      <div class="texture-bg bg-5 pull-right">
        <div class="hero-logo">
          <logo-right />
        </div>
        <div class="inner-texture"></div>
      </div>
      <!-- <div class="hero-logo-centred">
        <logo />
      </div> -->
      <div class="texture-bg bg-4 pull-left">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[2].asset)
              .width(imgRes.width)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
      <div class="texture-bg bg-3 pull-right">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[3].asset)
              .width(imgRes.width)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
      <div class="texture-bg bg-2 pull-left">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[4].asset)
              .width(imgRes.width)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
      <div class="texture-bg bg-1 pull-right">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[5].asset)
              .width(imgRes.width)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
    </div>
    <div id="reveal-left" class="image-reveal pull-left">
      <div class="inner-texture"></div>
    </div>
    <div id="reveal-right" class="image-reveal pull-right">
      <div class="inner-texture"></div>
    </div>
  </div>
</template>
<script>
import imageUrlBuilder from "@sanity/image-url";
import sanityClient from "../sanityClient";
import LogoLeft from "~/assets/circa_logo_left_nofill.svg?inline";
import LogoRight from "~/assets/circa_logo_right_nofill.svg?inline";

const urlBuilder = imageUrlBuilder(sanityClient);
export default {
  components: { LogoLeft, LogoRight },
  props: {
    animalImages: {
      type: Array,
      default: () => [],
    },
    imgRes: {
      type: Object,
      default: () => {},
    },
    scroll: {
      type: Object,
      default: () => {},
    },
  },
  mounted() {
    setTimeout(() => {
      this.initScroll();
    }, 1000);
  },
  methods: {
    initScroll() {
      const scrollContainer = document.getElementById("page-wrapper");
      const tl = gsap.timeline({
        scrollTrigger: {
          scroller: scrollContainer,
          trigger: "#scroll-trigger-1",
          start: "top top",
          scrub: true,
          markers: true,
        },
      });
      tl.to(
        "#reveal-right",
        {
          x: "100%",
          ease: "sine.inOut",
          duration: 0.4,
        },
        0
      );
      tl.to(
        "#reveal-left",
        {
          x: "-=100%",
          ease: "sine.inOut",
          duration: 0.4,
        },
        0
      );
      tl.to(
        ".bg-1",
        {
          x: "100%",
          ease: "sine.inOut",
          duration: 1.2,
        },
        0.2
      );
      tl.to(
        ".bg-1 .image-inner",
        {
          x: "-=40%",
          scale: 1.2,
          ease: "sine.inOut",
          duration: 1.2,
        },
        0.2
      );
      tl.to(
        ".bg-2",
        {
          x: "-=100%",
          ease: "sine.inOut",
          duration: 1.2,
        },
        0.2
      );
      tl.to(
        ".bg-2 .image-inner",
        {
          x: "+=40%",
          scale: 1.2,
          ease: "sine.inOut",
          duration: 1.2,
        },
        0.2
      );
      tl.to(
        ".bg-3",
        {
          x: "100%",
          ease: "sine.inOut",
          duration: 1.2,
        },
        1
      );
      tl.to(
        ".bg-3 .image-inner",
        {
          x: "-=40%",
          scale: 1.2,
          ease: "sine.inOut",
          duration: 1.2,
        },
        1
      );
      tl.to(
        ".bg-4",
        {
          x: "-=100%",
          ease: "sine.inOut",
          duration: 1.2,
        },
        1
      );
      tl.to(
        ".bg-4 .image-inner",
        {
          x: "+=40%",
          scale: 1.2,
          ease: "sine.inOut",
          duration: 1.2,
        },
        1
      );
      this.updateScroll();
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
