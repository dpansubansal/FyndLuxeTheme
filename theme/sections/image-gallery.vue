<template>
  <div class="section-wrapper full-width-section">
    <div class="gallery-container">
      <div class="card-container">
        <div class="top-items">
          <div class="title-block">
            <div :style="'color:' + global_config.props.text_heading_link_color" class="section-heading"
              v-if="
              (settings.props.title.value && settings.props.title.value.length > 0 && settings.props.layout.value !== 'horizontal1' && settings.props.layout.value !== 'horizontal2')">
              {{ settings.props.title.value }}
            </div>

          </div>
          <template v-if="settings.blocks.length > 0">
            <div class="grid6" v-if="settings.props.layout.value === 'grid'">
              <div v-for="(e, i) in filterImages" :key="i">
                <div class="grid6_item"><img :src="settings.blocks[i].props.image.value" /></div>
              </div>
            </div>
            <div class="grid5" v-if="settings.props.layout.value === 'grid5' && settings.blocks.length > 4">
              <div class=" grid5_item grid5_item_1"><img :src="settings.blocks[0].props.image.value" /></div>
              <div class=" grid5_item grid5_item_2"><img :src="settings.blocks[1].props.image.value" /></div>
              <div class=" grid5_item"><img :src="settings.blocks[2].props.image.value" /></div>
              <div class=" grid5_item"><img :src="settings.blocks[3].props.image.value" /></div>
              <div class=" grid5_item"><img :src="settings.blocks[4].props.image.value" /></div>
            </div>

            <div
              v-if="(settings.props.layout.value === 'horizontal1') || (settings.props.layout.value === 'horizontal2')">
              <div class="glide-cont" :class="'glide' + _uid" ref="glide">
                <div class="div1">
                  <div class="stickyContent">
                    {{ settings.props.title.value }}
                  </div>
                  <div data-glide-el="track" class="glide__track">
                    <div class="glide__slides" :class="{ 'ssr-slides-box': !checkisBrowser() && !isMounted }">
                      <div class="glide__slide" :class="index % 2 === 0 ? 'evenSlide' : 'oddSlide'"
                        v-for="(block, index) in settings.blocks" :key="index">
                        <gallery-item v-if="settings.props.layout.value === 'horizontal1'" :asp_ratio="'1'" :ishover="'hoverPls'"
                          :block="block" class="glideBlock"></gallery-item>
                        <gallery-item v-else :block="block" :asp_ratio="'3/4'" class="glideBlock" :ishover="'hoverPls'"></gallery-item>
                      </div>
                    </div>
                  </div>

                </div>
                <div class="div2">
                  <div class="glide__bullets" data-glide-el="controls[nav]"
                    v-if="settings.blocks.length > count_row">
                    <button class="glide__bullet" :data-glide-dir="'=' + entry"
                      v-for="(entry, index) in glidePaginate(settings.blocks.length, count_row)"
                      :key="index"></button>
                  </div>
                  <div class="arrows" v-if="
                    settings.blocks.length > 0 &&
                    settings.blocks.length > count_row
                  ">
                    <section>
                      <div class="prev-btn btn-nav-gallery" ref="prevArrow" @click="prevSlide">
                        <div class="icon icon-prev">
                          <arrowsvg />
                        </div>
                      </div>
                      <div class="next-btn btn-nav-gallery" ref="nextArrow" @click="nextSlide">
                        <div class="icon icon-next">
                          <arrowsvg />
                        </div>
                      </div>
                    </section>
                  </div>
                </div>
              </div>
            </div>
          </template>
          <template v-else>
            <placeholder-items :count="count_row * 2" :items_per_row="count_row" type="image" text=""
              :layout="settings.props.layout.value" />
          </template>
        </div>
      </div>
    </div>
  </div>
</template>
<!-- #region  -->

<settings>
{
    "name": "image_gallery",
    "label": "Image Gallery",
    "props": [
    {
            "id": "layout",
            "type": "select",
            "options": [
                {
                    "value": "grid",
                    "text": "Stack grid 6"
                },
                {
                    "value": "grid5",
                    "text": "Stack grid 5"
                },
                {
                    "value": "horizontal1",
                    "text": "Horizontal 1"
                },
                {
                    "value": "horizontal2",
                    "text": "Horizontal 2"
                }
            ],
            "default": "grid",
            "label": "Layout",
            "info": "Alignment of content"
        },
        {
            "type": "text",
            "id": "title",
            "default": "Timeless Fashion",
            "label": "Heading"
        }
    ],
    "blocks": [
        {
            "type": "gallery_image",
            "name": "Image",
            "props": [
                {
                    "type": "image_picker",
                    "id": "image",
                    "label": "Gallery Image",
                    "default": ""
                },
                {
                    "type": "text",
                    "id": "caption",
                    "label": "Image Caption",
                    "default": ""
                },
                {
                    "type": "url",
                    "id": "link",
                    "label": "Link",
                    "default": "",
                    "info": "Link to redirect"
                }
            ]
        }
    ],
    "preset":{
      "blocks":[
        {
          "name":"Image"
        },
        {
          "name":"Image"
        },
        {
          "name":"Image"
        },
        {
          "name":"Image"
        }
      ]
    }
}
</settings>
<!-- #endregion -->
<style scoped lang="less">
.section-wrapper {
  margin-top: var(--margin-top);
  margin-bottom: var(--margin-bottom);
}

.gallery-container {

  // margin: 20px 0px 30px 0px;
  @media @mobile {
    margin-top: 0;
  }

  .card-container {
    margin: 0;

    .top-items {
      // padding: 14px;
      border-radius: @border-radius;
      background: transparent;
      // margin: 10px 0 0 0;
    }

    .title-block {
      display: flex;
      text-transform: uppercase;
      text-align: center;
      box-sizing: border-box;
      position: relative;
      max-width: @page-width;
      .margin-0-auto();

      >div {
        flex: 0 0 100%;
      }
    }

    .link {
      position: absolute;
      line-height: 35px; //this is used to match the title-block height
      right: 0px;
      bottom: @title-margin-desktop;

      @media @tablet {
        display: none;
      }
    }
  }

  .arrows {
    //position: relative;
    //display: flex;
    //justify-content: flex-end;
    // top: 50%;
    //width: 100%;
    // margin: -40px 0 0 0;

    @media @mobile {
      display: none;
    }

    section {
      //position: relative;
      //width: 20%;
      //margin: 0 auto;
      display: flex;
      //padding: 0 20px;
      //box-sizing: border-box;
    }
  }

  .prev-btn {
    //margin-right: 22px;
  }

  .glide__bullets {
    position: relative;
    z-index: 2;
    margin-top: unset;
    bottom: unset;
    left: unset;
    list-style: none;
    transform: translateX(0%);
    padding-right: 5%;
    
    color: transparent;
    align-items: center;

    @media @mobile {
      display: none;
    }
  }

  .glide__bullet {
    background-color: unset;
    border: 1px solid @color-black;
    box-shadow: unset;

    &:hover {
      background-color: @color-black;
    }

    &.glide__bullet--active {
      background-color: @color-black;
    }
  }

  .glide__bullet {
    background-color: lightgrey;
    width: 100%;
    height: 1%;
    padding: 0;
    border-radius: 0%;
    border: 2px solid transparent;
    transition: all .3s ease-in-out;
    cursor: pointer;
    line-height: 0;
    //box-shadow: 0 .25em .5em 0 rgba(0,0,0,.1);
    margin: 0 0;
  }

  .glide__slide {
    height: auto;

    a {
      display: flex;
      height: 100%;
    }

    /deep/ .placeholder-svg {
      height: 99%;
      display: flex;

      svg {
        width: 100%;
      }
    }
  }

  .glide__slides.ssr-slides-box {
    touch-action: unset;
    overflow-x: auto;
  }

  .btn-nav-gallery {
    z-index: @layer;
    padding: unset;
    cursor: pointer;
    //width: 50px;
    display: flex;
    justify-content: center;
    transition: transform .2s;

    &:hover {
      transform: scale(1.2);
    }
  }

  .next-btn {
    margin-left: auto;
  }

  .icon {
    //display: inline-block;
    width: 45px;
    height: 45px;
    background-size: cover;
    border-radius: 50%;
    border: 1px solid lightgray;
  }

  .icon-next {

    transform: rotate(180deg);
  }

  .icon-prev {
    background-image: url(../assets/images/nav-arrow.svg);
  }

  //-----------------------------------GRID 6----------------------------------

  .grid6 {
    display: grid;
    grid-template-columns: auto auto auto;
    gap: 2%;
    align-items: center;
    padding: 0% 7%;

    @media screen and (max-width: 480px) {
      grid-template-columns: auto auto;
    }
  }


  .grid6_item>img {
    max-height: 100%;
    max-width: 100%;
    aspect-ratio: 1;
  }


  //-----------------------------------GRID 5----------------------------------

  .grid5 {
    display: grid;
    grid-template-columns: 60% auto auto;
    gap: 2%;
    align-items: center;
    padding: 0% 5%;
  }

  .grid5>.grid5_item {}

  .grid5_item_1 {
    grid-row-start: 1;
    grid-row-end: 3;
  }

  @media screen and (max-device-width: 780px) {
    .grid5_item_1 {

      grid-row-start: 1;
      grid-row-end: 2;
      grid-column-start: 1;
      grid-column-end: 3;
    }

    .grid5 {
      grid-template-columns: auto auto auto;

    }
  }

  @media screen and (max-device-width: 480px) {
    .grid5 {
      grid-template-columns: auto auto;

    }
  }

  .grid5_item>img {
    max-height: 100%;
    max-width: 100%;
    aspect-ratio: 1;
  }

  .grid5_item_2>img {
    @media screen and (min-device-width: 481px) and (max-device-width: 768px) {
      aspect-ratio: 1/2;
      object-fit: cover;
    }
  }

  .grid5_item_1>img {
    @media screen and (min-device-width: 768px) {
      aspect-ratio: 1.6;
    }
  }


  //------------------------------------For Animations---------------------------------


  .grid6_item,
  .grid5_item {
    overflow: hidden;
  }



  .grid6_item:hover>img,
  .grid5_item:hover>img {
    transform: scale(1.5);
  }
 
  //------------------------------------------------------------------------------



  .div1 {
    display: flex;
    flex-direction: row;

    @media screen and (max-width: 480px) {
      flex-direction: column;
    }
  }

  .stickyContent {
    width: 20%;
    align-items: center;
    display: flex;
    justify-content: center;
    font-family: Marcellus;
    font-weight: 400;
    font-size: 28px;
    line-height: 32px;
    padding: 3%;
  }

  .glide__track {
    width: 80%;
  }

  .div2 {
    display: grid;
    grid-template-columns: auto 110px;
    padding: 1% 3%;
  }

  .glideBlock {
    display: flex;
    flex-direction: column;
    position: relative;
    cursor: pointer;
    height: 100%;
    background-color: transparent;
    padding: 2%;
  }

  .evenSlide {
    margin-top: 1%;
  }



}
</style>
<script>
import { detectMobileWidth, glidePaginate } from "../helper/utils";
import { isBrowser, isNode } from "browser-or-node";
import groupList from "./../global/components/group-list.vue";
import galleryItem from "./../global/components/gallery-item.vue";
import Glide from '@glidejs/glide'
import '../../node_modules/@glidejs/glide/dist/css/glide.core.min.css';
import '../../node_modules/@glidejs/glide/dist/css/glide.theme.min.css';
import placeholderItemsVue from "../global/components/sections/placeholder-items.vue";
import arrowsvg from '../assets/images/nav-arrow.svg';

export default {
  props: ["settings", "global_config"],
  components: {
    arrowsvg,
    "gallery-item": galleryItem,
    "group-list": groupList,
    "placeholder-items": placeholderItemsVue,
  },
  watch: {
    settings: function (newVal, oldVal) {
      this.cleanupComponent();
      this.initializeComponent();
    },
  },
  computed: {
    filterImages: function () {
      return this.settings.blocks.filter((item, index) => index < 6)
    }
  },
  mounted() {
    this.initializeComponent();
  },
  data: function () {
    return {
      count_row: 3,
      isMounted: false,
      glideOptions: {
        type: 'slider',
        startAt: 0,
        gap: 0,
        bound:true,
        focusAt: 0,
        perView: 3,
        breakpoints: {
          1024: {
            perView: 3
          },
          600: {
            perView: 2
          },
          480: {
            perView: 1
          }
        }
      },
      carouselHandle: null
    };
  },
  methods: {
    checkisBrowser() {
      return isBrowser
    },
    glidePaginate,
    prevSlide() {
      let item_count = this.count_row;
      if (detectMobileWidth()) {
        if (this.carouselHandle.index - 1 >= 0) {
          this.carouselHandle.go(`=${this.carouselHandle.index - 1}`)
        }
      } else {
        if (this.carouselHandle.index - item_count >= 0) {
          this.carouselHandle.go(`=${this.carouselHandle.index - item_count}`)
        } else {
          this.carouselHandle.go(`<<`)
        }
      }
    },
    nextSlide() {
      let item_count = this.count_row;
      if (detectMobileWidth()) {
        if (this.carouselHandle.index + 1 >= this.settings.blocks.length - 1) {
          this.carouselHandle.go(`=${this.carouselHandle.index + 1}`)
        }
      } else {
        if (this.carouselHandle.index + item_count < this.settings.blocks.length) {
          this.carouselHandle.go(`=${this.carouselHandle.index + item_count}`)
        } else {
          this.carouselHandle.go(`>>`)
        }
      }
    },
    initCarousel() {
      //console.log("heyyy ypu", this.settings.props.layout.value);
      if (isNode || (this.settings.props.layout.value !== 'horizontal2' && this.settings.props.layout.value !== 'horizontal1') || this.carouselHandle) {
        return;
      }
      //console.log("Dipanshu Bansal");
      if (!this.$refs.glide) {
        setTimeout(() => { this.initCarousel() }, 1000)
        return;
      }
      this.$nextTick(() => {
        try {
          if (window.screen.width > 480 && window.screen.width <= 768) {
            this.glideOptions.gap = 40
          } else if (window.screen.width <= 480) {
            this.glideOptions.gap = 12
          }

          this.carouselHandle = new Glide(this.$refs.glide, this.glideOptions)
          let glideClass = this.$refs.glide.getAttribute('class')
          this.carouselHandle.on(['move.after'], () => {
            let allDots = document.querySelectorAll(`.${glideClass} [data-glide-dir]`)
            if (allDots && allDots.length > 0) {
              allDots.forEach(ele => {
                ele.classList.remove('glide__bullet--active')
              })
            }
            let currentDot = this.carouselHandle ? document.querySelectorAll(`.${glideClass} [data-glide-dir='=${this.carouselHandle.index}']`) : null;
            if (currentDot && currentDot.length > 0) {
              currentDot[0].classList.add('glide__bullet--active')
            }
          })
          this.carouselHandle.mount()
        } catch (ex) {
        }
      })
    },
    initializeComponent() {
      this.isMounted = true;
      if (window.screen.width > 600 && window.screen.width <= 1500) {
        this.count_row = 3
      } else if (window.screen.width > 480 && window.screen.width <= 600) {
        this.count_row = 2
      } else if (window.screen.width <= 480) {
        this.count_row = 1
      }
      this.glideOptions.perView = this.count_row;
      this.initCarousel()
    },
    cleanupComponent() {
      if (isBrowser && this.carouselHandle) {
        this.carouselHandle.destroy();
        this.carouselHandle = null;
      }
    }
  },
  beforeDestroy() {
    this.cleanupComponent()
  },
};
</script>
