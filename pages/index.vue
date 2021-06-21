<template>
  <div id="page-wrapper" ref="scroll-container" class="home page-wrapper">
    <div id="sticky-nav-target"></div>
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
          <div class="intro-texture-bg full-width">
            <div class="inner-texture" data-scroll data-scroll-speed="-2"></div>
          </div>
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
    <transition appear name="fade">
      <nav-desktop
        v-show="showUi"
        ref="nav"
        :scroll="scroll"
        data-scroll
        data-scroll-repeat="true"
        data-scroll-sticky="true"
        data-scroll-target="#hero-container"
      />
    </transition>
    <transition appear name="fade">
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
    </transition>
    <section
      id="about-wrapper"
      :class="['about__container', { 'is-mobile': isMobile }]"
      data-scroll
      data-scroll-call="about"
    >
      <div class="about-texture-bg full-width">
        <div class="inner-texture" data-scroll data-scroll-speed="-2"></div>
      </div>
      <div
        v-if="isMobile"
        class="about__title title-reveal is-mobile"
        data-scroll
        data-splitting
        data-scroll-offset="20%"
      >
        <block-content
          :blocks="about.aboutTitle"
          :serializers="serializers"
        ></block-content>
      </div>
      <about-scroller
        :about="about"
        :scroll="scroll"
        :is-mobile="isMobile"
      ></about-scroller>
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
      <div
        v-if="isMobile"
        class="about__body body-copy is-mobile"
        data-scroll
        data-scroll-speed="2"
      >
        <h2 class="subhead">Our Story</h2>
        <block-content :blocks="about.aboutBody"></block-content>
        <!-- <a class="cta-link">Lets talk about the details – get in touch</a> -->
      </div>

      <div v-if="!isMobile" class="about__content">
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
            backgroundImage:
              imgRes.width > 1
                ? `url('${urlFor(services.servicesImage.asset)
                    .width(
                      isMobile && imgRes.width < 1000
                        ? imgRes.width
                        : Math.floor(imgRes.width / 3)
                    )
                    .height(Math.floor(imgRes.height / 2))
                    .format('jpg')
                    .quality(50)
                    .saturation(-100)
                    .url()}')`
                : 'none',
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
          <div class="services__icons-row" data-scroll data-scroll-offset="20%">
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
    <section
      id="clients-wrapper"
      :class="['clients__container', { 'is-mobile': isMobile }]"
      data-scroll
    >
      <div class="clients__content">
        <div
          class="clients__body body-copy"
          data-scroll
          data-scroll-offset="30%"
        >
          <block-content :blocks="clients.clientsBody"></block-content>
        </div>
        <!-- <div class="clients__logos-grid"></div> -->
        <div
          v-if="!isMobile"
          class="clients__logos-scroller"
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
        <div v-else class="clients__logos--mobile">
          <div class="logos-grid-mobile">
            <figure
              v-for="(client, i) in clients.clients"
              :key="i"
              class="logo-inner"
              :style="{
                backgroundImage: `url('${urlFor(client.logo)
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
    <section id="work-wrapper" class="work__container" data-scroll>
      <div
        class="section-hero-image__wrapper work"
        data-scroll
        data-scroll-offset="20%"
      >
        <figure
          class="section-hero-image__inner work"
          data-scroll
          data-scroll-direction="horizontal"
          data-scroll-speed="-1"
          :alt="work.workImage.title"
          :style="{
            backgroundImage:
              imgRes.width > 1
                ? `url('${urlFor(work.workImage.asset)
                    .width(
                      isMobile && imgRes.width < 1000
                        ? imgRes.width
                        : Math.floor(imgRes.width / 3)
                    )
                    .height(Math.floor(imgRes.height / 2))
                    .format('jpg')
                    .quality(70)
                    .saturation(-100)
                    .url()}')`
                : 'none',
          }"
        ></figure>
      </div>
      <div
        class="work-texture-bg pull-right"
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
        class="work-texture-bg pull-left"
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
      <div class="work__content">
        <div
          class="section-caption-wrapper"
          data-scroll
          data-scroll-offset="30%"
        >
          <h3 class="section-caption">Our work</h3>
        </div>
        <div
          class="work__title title-reveal"
          data-scroll
          data-splitting
          data-scroll-offset="30%"
        >
          <block-content
            :blocks="work.workTitle"
            :serializers="serializers"
          ></block-content>
        </div>
        <div
          class="work__body body-copy"
          data-scroll
          data-scroll-speed="2"
          data-scroll-offset="30%"
        >
          <block-content :blocks="work.workBody"></block-content>
          <a
            class="cta-link"
            @click.prevent="
              scrollTo('#connect-wrapper', {
                offset: 0,
                duration: 1000,
              })
            "
            >{{ work.workCta }}</a
          >
        </div>

        <!-- CASE STUDIES -->
      </div>
    </section>
    <section
      v-if="ready"
      class="case-studies__container"
      data-scroll
      data-scroll-call="cases"
      data-scroll-repeat
      :data-scroll-offset="navOffset"
    >
      <case-study
        v-for="project in work.caseStudies"
        :key="project.product"
        :content="project"
        :scroll="scroll"
        :img-res="imgRes"
      ></case-study>
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
            backgroundImage:
              imgRes.width > 1
                ? `url('${urlFor(connect.connectImageLeft.asset)
                    .width(
                      isMobile && imgRes.width < 1000
                        ? imgRes.width
                        : Math.floor(imgRes.width / 2)
                    )
                    .height(Math.floor(imgRes.height))
                    .format('jpg')
                    .quality(70)
                    .saturation(-100)
                    .url()}')`
                : 'none',
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
            backgroundImage:
              imgRes.width > 1
                ? `url('${urlFor(connect.connectImageRight.asset)
                    .width(
                      isMobile && imgRes.width < 1000
                        ? imgRes.width
                        : Math.floor(imgRes.width / 2)
                    )
                    .height(Math.floor(imgRes.height))
                    .format('jpg')
                    .quality(70)
                    .saturation(-100)
                    .url()}')`
                : 'none',
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
      data-scroll-target="#sticky-nav-target"
      :active="navActive"
      :scroll="scroll"
      :dark="dark"
      @hook:mounted="setNavOffset"
    />
    <app-footer />
  </div>
</template>

<script>
import mobile from "is-mobile";
import imageUrlBuilder from "@sanity/image-url";
import sanityClient from "../sanityClient";
import Arrow from "~/assets/down_arrow.svg?inline";
import copyline from "~/components/span.vue";
import Logo from "~/assets/circa_logo_nofill.svg?inline";

const urlBuilder = imageUrlBuilder(sanityClient);

if (typeof window === "undefined") {
  global.window = { innerWidth: 0, innerHeight: 0, devicePixelRatio: 0 };
}

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
    "work": {
      workTitle, workBody, workCta, workImage,
      caseStudies[],
    },
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
      scroll: {
        update: () => {
          console.log("scroll not initialized");
        },
        destroy: () => {
          console.log("scroll not initialized destroy");
        },
      },
      showUi: false,
      showPrompt: false,
      ready: false,
      scrollInit: false,
      imgRes: { width: 1, height: 1, dpr: 1 },
      navOffset: "100%, 60",
      isMobile: "",
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
        {
          property: "og:locale",
          content: "en_GB",
          vmid: "og:locale",
        },
        {
          property: "og:type",
          content: "website",
          vmid: "og:type",
        },
        {
          property: "og:url",
          content: "https://www.circa-healthcare.co.uk",
          vmid: "og:url",
        },
        {
          property: "og:site_name",
          content: "Circa Healthcare",
          vmid: "og:site_name",
        },
        {
          property: "og:image",
          content: "circa_thumbnail_large.jpg",
          vmid: "og:image",
        },
        {
          property: "og:image:width",
          content: "1200",
          vmid: "og:image_width",
        },
        {
          property: "og:image:height",
          content: "630",
          vmid: "og:image_width",
        },
        {
          property: "og:title",
          content: title,
          vmid: "og:title",
        },
        {
          property: "og:description",
          content: description,
          vmid: "og:description",
        },
        {
          property: "twitter:card",
          content: "summary_large_image",
          vmid: "twitter:card",
        },
        {
          property: "twitter:title",
          content: title,
          vmid: "twitter:title",
        },
        {
          property: "twitter:description",
          content: description,
          vmid: "twitter:description",
        },
        {
          property: "twitter:image",
          content: "circa_thumbnail_large.jpg",
          vmid: "twitter:image",
        },
      ],
    };
  },
  computed: {
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
    if (mobile({ tablet: true, featureDetect: true })) {
      this.isMobile = true;
    } else {
      this.isMobile = false;
    }
    gsap.registerPlugin(ScrollTrigger);
    this.setImgRes();
    this.initScroll();
  },
  beforeDestroy() {
    // const that = this;
    // ScrollTrigger.removeEventListener("refresh", () => that.scroll.update());
    ScrollTrigger.kill();
    console.log("destroy scroll");
    window.removeEventListener("resize", this.handleResize);
    this.scroll.destroy();
    this.scroll = null;
  },
  methods: {
    init() {
      this.initScroll();
    },
    urlFor(source) {
      return urlBuilder.image(source);
    },
    setImgRes() {
      const width = window.innerWidth;
      const height = window.innerHeight;
      const dpr = window.devicePixelRatio;
      const res = {};
      if (width > 1440) {
        res.width = 1920;
        res.height = 1080;
      } else if (width > 1024) {
        res.width = 1440;
        res.height = 900;
      } else if (width >= 768) {
        res.width = 800;
      }
      res.height = Math.round(height * 0.8);
      if (this.isMobile) {
        res.width = width;
        res.height = height;
      }
      this.imgRes = { ...res, dpr };
    },
    initScroll() {
      const el = this.$refs["scroll-container"];
      this.scroll = new this.LocomotiveScroll({
        el,
        smooth: true,
        getDirection: true,
      });
      setTimeout(() => {
        this.updateScroll();
      }, 500);

      this.scrollInit = true;
      this.$nextTick(() => this.initScrollTrigger());
    },
    initScrollTrigger() {
      console.log("BEGIN SCROLLTRIGGER INIT");
      const el = this.$refs["scroll-container"];
      this.scroll.on("scroll", ScrollTrigger.update);
      const that = this;
      ScrollTrigger.scrollerProxy(el, {
        scrollTop(value) {
          return arguments.length
            ? that.scroll.scrollTo(value, 0, 0)
            : that.scroll.scroll.instance.scroll.y;
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
      // ScrollTrigger.addEventListener("refresh", () => that.scroll.update());
      this.updateScroll();
      this.$nextTick(() => {
        this.initScrollEvents();
      });
    },
    setNavOffset() {
      console.log("SET NAV OFFSET");
      const nav = document.getElementById("nav-sticky");
      console.log(nav);
      const navHeight = nav.offsetHeight;
      this.navOffset = `${window.innerHeight - navHeight}, ${navHeight}`;
    },
    initScrollEvents() {
      console.log("BEGIN SCROLL EVENTS INIT");
      window.addEventListener("resize", this.handleResize);

      this.scroll.on("call", (value, way, obj) => {
        if (value === "hero") {
          // console.log("HERO");
          if (way === "exit") {
            this.navActive = true;
          } else {
            this.navActive = false;
          }
        }
        if (value === "cases") {
          console.log(value, way, obj);
          if (way === "enter") {
            this.dark = true;
          } else if (way === "exit") {
            this.dark = false;
          }
        }
      });
    },
    updateScroll() {
      console.log("update scroll index");
      ScrollTrigger.refresh();
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
      if (this.scrollInit === false) {
        setTimeout(() => {
          this.onLoad();
        }, 50);
      } else if (this.scrollInit === true) {
        this.ready = true;
        console.log("ONLOAD INDEX");
        setTimeout(() => {
          this.showUi = true;
          document.body.style.setProperty("--bg-root", "#00304d");
          this.updateScroll();
        }, 500);
        setTimeout(() => {
          this.showPrompt = true;
          this.updateScroll();
        }, 3000);
        this.$nextTick(() => {
          this.splitText();
        });
      }
    },
  },
};
</script>
