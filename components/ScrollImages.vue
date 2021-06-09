<template>
  <div
    class="hero__background"
    data-scroll
    data-scroll-repeat="true"
    data-scroll-sticky="true"
    data-scroll-target="#hero"
  >
    <div class="hero__images">
      <div class="texture-wrapper">
        <div
          class="texture-bg bg-1"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="1"
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
      <div class="texture-wrapper">
        <div
          class="texture-bg bg-2"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-1"
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
      <div class="texture-wrapper">
        <div
          class="texture-bg bg-3"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="10"
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
      <div class="texture-wrapper">
        <div
          class="texture-bg bg-4"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-10"
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
  },
  methods: {
    urlFor(source) {
      return urlBuilder.image(source);
    },
  },
};
</script>
