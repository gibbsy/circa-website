<template>
  <div
    class="hero__background"
    data-scroll
    data-scroll-repeat="true"
    data-scroll-sticky="true"
    data-scroll-target="#hero"
  >
    <div class="hero__bg-inner">
      <div class="hero__images">
        <div
          class="texture-bg bg-6 pull-left"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="0.2"
          data-scroll-delay="0.05"
        >
          <div
            class="image-inner"
            data-scroll
            data-scroll-direction="horizontal"
            data-scroll-speed="-0.1"
            data-scroll-delay="0.05"
            :style="{
              backgroundImage: `url('${urlFor(animalImages[1].asset)
                .width(imgRes.width)
                .height(imgRes.height)
                .dpr(imgRes.dpr)
                .format('jpg')
                .quality(70)
                .url()}')`,
            }"
          ></div>
        </div>
        <div
          class="texture-bg bg-5 pull-right"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-0.2"
          data-scroll-delay="0.05"
        >
          <div
            class="image-inner"
            data-scroll
            data-scroll-direction="horizontal"
            data-scroll-speed="0.1"
            data-scroll-delay="0.05"
            :style="{
              backgroundImage: `url('${urlFor(animalImages[0].asset)
                .width(imgRes.width)
                .height(imgRes.height)
                .dpr(imgRes.dpr)
                .auto('jpg')
                .quality(70)
                .url()}')`,
            }"
          ></div>
        </div>
        <div
          class="texture-bg bg-4 pull-left"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="10"
          data-scroll-delay="0.1"
        >
          <div
            class="image-inner"
            data-scroll
            data-scroll-direction="horizontal"
            data-scroll-speed="-5"
            data-scroll-delay="0.1"
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
        <div
          class="texture-bg bg-3 pull-right"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-10"
          data-scroll-delay="0.1"
        >
          <div
            class="image-inner"
            data-scroll
            data-scroll-direction="horizontal"
            data-scroll-speed="5"
            data-scroll-delay="0.1"
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
        <div
          class="texture-bg bg-2 pull-left"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="30"
          data-scroll-delay="0.1"
        >
          <div
            class="image-inner"
            data-scroll
            data-scroll-direction="horizontal"
            data-scroll-speed="-10"
            data-scroll-delay="0.1"
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
        <div
          class="texture-bg bg-1 pull-right"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-30"
          data-scroll-delay="0.1"
        >
          <div
            class="image-inner"
            data-scroll
            data-scroll-direction="horizontal"
            data-scroll-speed="10"
            data-scroll-delay="0.1"
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
      <div
        class="image-reveal pull-left"
        data-scroll
        data-scroll-direction="horizontal"
        data-scroll-speed="60"
        data-scroll-delay="0.06"
      ></div>
      <div
        class="image-reveal pull-right"
        data-scroll
        data-scroll-direction="horizontal"
        data-scroll-speed="-60"
        data-scroll-delay="0.06"
      ></div>
    </div>
  </div>
</template>
<script>
import imageUrlBuilder from "@sanity/image-url";
import sanityClient from "../sanityClient";
const urlBuilder = imageUrlBuilder(sanityClient);
export default {
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
  methods: {
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
