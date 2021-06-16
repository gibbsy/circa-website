<template>
  <div id="page-wrapper" ref="scroll" class="home page-wrapper">
    <section
      id="hero-container"
      class="hero__container"
      data-scroll
      data-scroll-call="hero"
      data-scroll-repeat="true"
    >
      <div
        :class="['hero__background', { dark: showUi }]"
        data-scroll
        data-scroll-repeat="true"
        data-scroll-sticky="true"
        data-scroll-target="#hero-container"
        data-scroll-speed="-10"
      >
        <HeroVideo
          player-id="textures"
          vimeo-id="563685796"
          :scroll="scroll"
          :ready-fn="onLoad"
        ></HeroVideo>
      </div>
      <article
        id="hero-text"
        :class="['hero__content', { hide: !ready }]"
        data-scroll
        data-splitting
      >
        <div class="hero__title" data-scroll data-scroll-speed="0.2">
          <div :class="['title-inner', { shift: !showPrompt }]">
            <block-content
              :blocks="hero.heroTitle"
              :serializers="serializers"
            ></block-content>
          </div>
          <div :class="['hero__scroll-prompt', { on: showPrompt }]">
            <p
              class="prompt"
              data-scroll
              data-scroll-repeat="true"
              data-scroll-offset="0,50%"
            >
              {{ hero.heroPrompt }}
            </p>
            <div
              class="arrow-wrapper"
              data-scroll
              data-scroll-repeat="true"
              data-scroll-offset="-100,50%"
            >
              <arrow />
            </div>
          </div>
        </div>
        <div id="intro-wrapper" class="hero__intro" data-scroll>
          <div
            class="hero__intro-inner"
            data-scroll
            data-scroll-sticky
            data-scroll-target="#intro-wrapper"
          >
            <div
              class="intro__text-reveal"
              data-scroll
              data-scroll-offset="20%"
            >
              <block-content :blocks="hero.heroBody"></block-content>
            </div>
          </div>
        </div>
      </article>
    </section>
    <nav-desktop
      v-show="showUi"
      ref="nav"
      :scroll="scroll"
      data-scroll
      data-scroll-repeat="true"
      data-scroll-sticky="true"
      data-scroll-target="#hero-container"
    />
    <div
      v-show="showUi"
      ref="logo-peel"
      class="circa-logo logo-corner-left"
      aria-label="circa Logo"
      data-scroll
      data-scroll-repeat="true"
      data-scroll-sticky="true"
      data-scroll-target="#hero-container"
    >
      <nuxt-link to="/">
        <logo />
      </nuxt-link>
    </div>
    <section
      id="about-wrapper"
      class="about__container"
      data-scroll
      data-scroll-call="about"
    >
      <div class="about-texture-bg full-width">
        <div class="inner-texture" data-scroll data-scroll-speed="-2"></div>
      </div>
      <about-scroller :about="about" :scroll="scroll"></about-scroller>
      <div
        class="about-texture-bg pull-right"
        data-scroll
        data-scroll-direction="horizontal"
        data-scroll-speed="2"
      >
        <div
          class="inner-texture"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-1"
        ></div>
      </div>
      <div class="about__content">
        <div
          class="about__title title-reveal"
          data-scroll
          data-splitting
          data-scroll-offset="20%"
        >
          <block-content
            :blocks="about.aboutTitle"
            :serializers="serializers"
          ></block-content>
        </div>
        <div
          class="about__body body-copy"
          data-scroll
          data-scroll-speed="2"
          data-scroll-offset="150%"
        >
          <h2 class="subhead">Our Story</h2>
          <block-content :blocks="about.aboutBody"></block-content>
          <!-- <a class="cta-link">Lets talk about the details – get in touch</a> -->
        </div>
      </div>
    </section>
    <section id="services-wrapper" class="services__container" data-scroll>
      <div
        class="section-hero-image__wrapper services"
        data-scroll
        data-scroll-offset="20%"
      >
        <figure
          class="section-hero-image__inner services"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-1"
          :alt="services.servicesImage.title"
          :style="{
            backgroundImage: `url('${urlFor(services.servicesImage.asset)
              .width(imgRes.width)
              .format('jpg')
              .quality(50)
              .saturation(-100)
              .url()}')`,
          }"
        ></figure>
      </div>
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
      <div
        class="services-texture-bg pull-left"
        data-scroll
        data-scroll-direction="horizontal"
        data-scroll-speed="-2"
      >
        <div
          class="inner-texture"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="2"
        ></div>
      </div>
      <div class="services__content">
        <div
          class="section-caption-wrapper"
          data-scroll
          data-scroll-offset="30%"
        >
          <h3 class="section-caption">What we do</h3>
        </div>
        <div
          class="services__title title-reveal"
          data-scroll
          data-splitting
          data-scroll-offset="30%"
        >
          <block-content
            :blocks="services.servicesTitle"
            :serializers="serializers"
          ></block-content>
        </div>
        <div
          class="services__body body-copy"
          data-scroll
          data-scroll-speed="2"
          data-scroll-offset="30%"
        >
          <block-content :blocks="services.servicesBody"></block-content>
        </div>
        <div class="services__icons">
          <div
            class="services__icons-row"
            data-scroll
            data-scroll-offset="20%"
            data-scroll-repeat
          >
            <div class="services__icon-wrapper">
              <figure class="icon-inner strategy"></figure>
              <h3 class="service-title">Strategy</h3>
            </div>
            <div class="services__icon-wrapper">
              <figure class="icon-inner creative"></figure>
              <h3 class="service-title">Creative</h3>
            </div>
            <div class="services__icon-wrapper">
              <figure class="icon-inner delivery"></figure>
              <h3 class="service-title">Delivery</h3>
            </div>
          </div>
        </div>
        <div
          class="services__cta cta-centred"
          data-scroll
          data-scroll-offset="30%"
        >
          <a
            class="cta-link"
            @click.prevent="
              scrollTo('#connect-wrapper', {
                offset: 0,
                duration: 1000,
              })
            "
            >Lets talk about the details – get in touch</a
          >
        </div>
      </div>
    </section>
    <section id="clients-wrapper" class="clients__container" data-scroll>
      <div class="clients__content">
        <div
          class="clients__body body-copy"
          data-scroll
          data-scroll-offset="30%"
        >
          <block-content :blocks="clients.clientsBody"></block-content>
        </div>
        <div
          class="clients__logos"
          data-scroll
          data-scroll-speed="-2"
          data-scroll-offset="20%"
          data-scroll-repeat
        >
          <div
            class="logos-row-1 logo-row"
            data-scroll
            data-scroll-direction="horizontal"
            data-scroll-speed="20"
          >
            <div
              v-for="(logo, i) in clientLogos.r1"
              :key="i"
              class="logo-wrapper"
            >
              <figure
                class="logo-inner"
                :style="{
                  backgroundImage: `url('${urlFor(logo.logo)
                    .width(560)
                    .format('jpg')
                    .quality(50)
                    .saturation(-100)
                    .bg('fff')
                    .url()}')`,
                }"
              ></figure>
            </div>
          </div>
          <div
            class="logos-row-2 logo-row"
            data-scroll
            data-scroll-direction="horizontal"
            data-scroll-speed="-20"
          >
            <div
              v-for="(logo, i) in clientLogos.r2"
              :key="i"
              class="logo-wrapper"
            >
              <figure
                class="logo-inner"
                :style="{
                  backgroundImage: `url('${urlFor(logo.logo)
                    .width(560)
                    .format('jpg')
                    .quality(50)
                    .saturation(-100)
                    .bg('fff')
                    .url()}')`,
                }"
              ></figure>
            </div>
          </div>
        </div>
        <div
          class="clients__cta cta-centred"
          data-scroll
          data-scroll-offset="20%"
        >
          <a
            class="cta-link"
            @click.prevent="
              scrollTo('#connect-wrapper', {
                offset: 0,
                duration: 1000,
              })
            "
            >Are you ready to chat?</a
          >
        </div>
      </div>
    </section>
    <section id="connect-wrapper" class="connect__container" data-scroll>
      <div
        class="section-hero-image__wrapper connect --left"
        data-scroll
        data-scroll-direction="horizontal"
        data-scroll-speed="-2"
        data-scroll-offset="10%"
      >
        <figure
          class="section-hero-image__inner connect --left"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-1"
          :alt="connect.connectImageLeft.title"
          :style="{
            backgroundImage: `url('${urlFor(connect.connectImageLeft.asset)
              .width(imgRes.width * 0.5)
              .height(imgRes.height)
              .format('jpg')
              .quality(50)
              .saturation(-100)
              .url()}')`,
          }"
        ></figure>
      </div>
      <div
        class="section-hero-image__wrapper connect --right"
        data-scroll
        data-scroll-direction="horizontal"
        data-scroll-speed="2"
        data-scroll-offset="10%"
      >
        <figure
          class="section-hero-image__inner connect --right"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="1"
          :alt="connect.connectImageRight.title"
          :style="{
            backgroundImage: `url('${urlFor(connect.connectImageRight.asset)
              .width(imgRes.width * 0.5)
              .height(imgRes.height)
              .format('jpg')
              .quality(50)
              .saturation(-100)
              .url()}')`,
          }"
        ></figure>
      </div>

      <div class="connect__content">
        <div class="connect__content-inner">
          <div
            class="connect__title title-reveal"
            data-scroll
            data-splitting
            data-scroll-offset="30%"
          >
            <block-content
              :blocks="connect.connectTitle"
              :serializers="serializers"
            ></block-content>
          </div>
          <div
            class="connect__body body-copy"
            data-scroll
            data-scroll-offset="30%"
          >
            <block-content :blocks="connect.connectIntro"></block-content>
          </div>
          <div class="connect__details" data-scroll data-scroll-offset="20%">
            <div
              v-for="location in connect.contactDetails"
              :key="location.title"
              class="connect-loc"
            >
              <h3>{{ location.title }}</h3>
              <a class="contact-details"
                ><h3>{{ location.email }}</h3></a
              >
              <a class="contact-details"
                ><h3>{{ location.phone }}</h3></a
              >
              <block-content
                :blocks="location.address"
                :serializers="serializers"
              ></block-content>
            </div>
          </div>
        </div>
      </div>
    </section>
    <nav-sticky
      data-scroll
      data-scroll-sticky
      data-scroll-target="#page-wrapper"
      :active="navActive"
      :scroll="scroll"
      :dark="dark"
    />
    <app-footer />
  </div>
</template>

<script>
// import NavDesktop from "../components/NavDesktop.vue";
// import mobile from "is-mobile";
import imageUrlBuilder from "@sanity/image-url";
import sanityClient from "../sanityClient";
import Arrow from "~/assets/down_arrow.svg?inline";
import copyline from "~/components/span.vue";
import Logo from "~/assets/circa_logo_nofill.svg?inline";

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
      aboutTitle, aboutBody, aboutStats, aboutImages[]
    },
    "services": {
      servicesTitle, servicesBody, servicesImage, servicesList
    },
    "clients": {
      clientsBody, clients[] {
        name, logo
      }
    },
    caseStudies,
    "connect": {
      connectTitle, connectIntro, connectImageLeft, connectImageRight, contactDetails
    }
},
"legals": *[_type == "legalsPage" ]{ title, "slug": slug.current }
}`;
export default {
  components: {
    Logo,
    Arrow,
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
      dark: false,
      resizeTimeout: 0,
      scroll: {},
      showUi: false,
      showPrompt: false,
      ready: false,
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
    clientLogos() {
      const logos = this.clients.clients;
      const r1 = logos.slice(0, logos.length / 2);
      const r2 = logos.slice(logos.length / 2);
      return {
        r1,
        r2,
      };
    },
  },
  mounted() {
    gsap.registerPlugin(ScrollTrigger);
    this.$nextTick(() => {
      this.init();
    });
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
      const scroller = new this.LocomotiveScroll({
        el,
        smooth: true,
        getDirection: true,
      });
      setTimeout(() => {
        this.updateScroll();
      }, 500);

      scroller.on("scroll", ScrollTrigger.update);
      ScrollTrigger.scrollerProxy(el, {
        scrollTop(value) {
          return arguments.length
            ? scroller.scrollTo(value, 0, 0)
            : scroller.scroll.instance.scroll.y;
        }, // we don't have to define a scrollLeft because we're only scrolling vertically.
        getBoundingClientRect() {
          return {
            top: 0,
            left: 0,
            width: window.innerWidth,
            height: window.innerHeight,
          };
        },
        // LocomotiveScroll handles things completely differently on mobile devices - it doesn't even transform the container at all! So to get the correct behavior and avoid jitters, we should pin things with position: fixed on mobile. We sense it by checking to see if there's a transform applied to the container (the LocomotiveScroll-controlled element).
        pinType: document.querySelector("#page-wrapper").style.transform
          ? "transform"
          : "fixed",
      });
      ScrollTrigger.addEventListener("refresh", () => scroller.update()); // locomotive-scroll
      ScrollTrigger.refresh();
      this.scroll = scroller;
      this.$nextTick(() => {
        this.initScrollEvents();
      });
    },
    initScrollEvents() {
      window.addEventListener("resize", this.handleResize);
      this.scroll.on("call", (value, way, obj) => {
        if (value === "hero") {
          // console.log("HERO");
          console.log(way);
          if (way === "exit") {
            this.navActive = true;
          } else {
            this.navActive = false;
          }
        }
      });
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
    onLoad() {
      this.ready = true;
      /*   const logoEl = this.$refs["logo-peel"];
      gsap.fromTo(
        logoEl,
        { x: "-100%" },
        { x: 0, duration: 1, ease: "Power2.easeOut" }
      ); */
      setTimeout(() => {
        this.showUi = true;
        document.body.style.setProperty("--bg-root", "#00304d");
        ScrollTrigger.refresh();
        this.updateScroll();
      }, 500);
      setTimeout(() => {
        this.showPrompt = true;
        ScrollTrigger.refresh();
        this.updateScroll();
      }, 3000);
      this.$nextTick(() => {
        this.splitText();
        // this.scroll.start();
        ScrollTrigger.refresh();
        this.updateScroll();
      });
    },
  },
};
</script>
