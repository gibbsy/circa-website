<template>
  <div :class="['hero__background', { loaded: !loading }]">
    <div v-if="imgRes.width > 1" id="image-container" class="hero__images">
      <!--   <div class="texture-bg bg-6 pull-left">
        <div class="inner-texture"></div>
      </div>
      <div class="texture-bg bg-5 pull-right">
        <div class="inner-texture"></div>
      </div> -->
      <div class="texture-bg bg-6 pull-left">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[6].asset)
              .width(imgRes.width / 2)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
      <div class="texture-bg bg-5 pull-right">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[0].asset)
              .width(imgRes.width / 2)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
      <div class="texture-bg bg-4 pull-left">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[3].asset)
              .width(imgRes.width / 2)
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
            backgroundImage: `url('${urlFor(animalImages[6].asset)
              .width(imgRes.width / 2)
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
            backgroundImage: `url('${urlFor(animalImages[5].asset)
              .width(imgRes.width / 2)
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
            backgroundImage: `url('${urlFor(animalImages[4].asset)
              .width(imgRes.width / 2)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
      <div id="reveal-left" class="texture-bg image-reveal pull-left">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[10].asset)
              .width(imgRes.width / 2)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
      <div id="reveal-right" class="texture-bg image-reveal pull-right">
        <div
          class="image-inner"
          :style="{
            backgroundImage: `url('${urlFor(animalImages[9].asset)
              .width(imgRes.width / 2)
              .height(imgRes.height)
              .dpr(imgRes.dpr)
              .format('jpg')
              .quality(70)
              .url()}')`,
          }"
        ></div>
      </div>
    </div>
    <!--     <div id="reveal-left" class="image-reveal pull-left">
      <div class="inner-texture"></div>
    </div>
    <div id="reveal-right" class="image-reveal pull-right">
      <div class="inner-texture"></div>
    </div> -->
    <transition appear name="slide-down">
      <nav-desktop ref="nav" :scroll="scroll" />
    </transition>
    <div
      ref="logo-peel"
      class="circa-logo logo-corner-left"
      aria-label="circa Logo"
    >
      <nuxt-link to="/">
        <logo />
      </nuxt-link>
    </div>
  </div>
</template>
<script>
import imageUrlBuilder from "@sanity/image-url";
import sanityClient from "../sanityClient";
import Logo from "~/assets/circa_logo_nofill.svg?inline";

const urlBuilder = imageUrlBuilder(sanityClient);
export default {
  components: { Logo },
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
    loadFn: {
      type: Function,
      default: () => {},
    },
  },
  data() {
    return {
      loading: true,
    };
  },
  mounted() {
    const imgLoad = imagesLoaded(
      "#image-container",
      { background: true },
      () => {
        const that = this;
        setTimeout(() => {
          that.loading = false;
          that.loadFn();
          console.log("imgs loaded");
        }, 1000);
      }
    );
    imgLoad.on("progress", function (instance, image) {
      const result = image.isLoaded ? "loaded" : "broken";
      console.log("image is " + result + " for " + image.img.src);
    });
    this.initScroll();
  },
  methods: {
    initScroll() {
      const scrollContainer = document.getElementById("page-wrapper");
      const logoEl = this.$refs["logo-peel"];
      gsap.fromTo(
        logoEl,
        { x: "-100%" },
        { x: 0, duration: 1, ease: "Power2.easeOut" }
      );
      const tl = gsap.timeline({
        scrollTrigger: {
          scroller: scrollContainer,
          trigger: "#scroll-trigger-1",
          start: "top top",
          scrub: true,
          // markers: true,
          pin: ".hero__background",
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
        "#reveal-right .image-inner",
        {
          x: "-=40%",
          scale: 1.2,
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
        "#reveal-left .image-inner",
        {
          x: "+=40%",
          scale: 1.2,
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
