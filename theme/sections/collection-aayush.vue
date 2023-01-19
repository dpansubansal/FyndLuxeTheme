<template>
    <div
      :class="{
        'section-main-container': !getSectionValue(settings,'full_width'),
        'full-width-section': getSectionValue(settings,'full_width'),
      }"
    >
      <div class="gallery-container">     
        <div class="card-container">
          <div class="top-items">
            <div class="title-block">
              <div
                :style="'color:' + global_config.props.text_heading_link_color"
                class="section-heading"
                v-if="
                  (getSectionValue(settings,'title') &&
                  getSectionValue(settings,'title').length > 0) ||getSectionValue(settings,'cta_text')
                "
              >{{ getSectionValue(settings,'title') }}</div>
            </div>
            <template>
              <div  v-if="getSectionValue(settings,'desktop_layout') === 'style1'">
                <div class="ayush">
                  <fy-product-card 
                    :product="products[0]"
                    :showWishlist="true"
                    :context="context"
                    :global_config="global_config"
                  ></fy-product-card>
                </div> 
                <div class="pr-img">           
                  <div v-for="(product,i) in products" :key="i">
                    <div class="full" v-if="i<8">                      
                      <fy-product-card 
                        :product="product"
                        :showWishlist="true"                      
                        :context="context"
                        :global_config="global_config"                      
                      ></fy-product-card>
                    </div>   
                    <div class="tab" v-if="i<4">
                      <fy-product-card 
                        :product="product"
                        :showWishlist="true"
                        :context="context"
                        :global_config="global_config"
                      ></fy-product-card>
                    </div>  
                    <div class="mob" v-if="i<4">
                      <fy-product-card 
                        :product="product"
                        :showWishlist="true"
                        :context="context"
                        :global_config="global_config"
                      ></fy-product-card>
                    </div>                     
                  </div>
                </div> 
              </div>
              <div v-if="getSectionValue(settings,'desktop_layout') === 'style2'">
                <div v-if="products.length>0" class="glide-cont" :class="'glide'+ _uid" ref="glide">
                  <div data-glide-el="track" class="glide__track">
                    <div class="glide__slides" :class="{ 'ssr-slides-box': !checkisBrowser() && !isMounted }">
                      <div class="glide__slide" 
                        v-for="product in products" 
                        :key="product"
                        >
                        <fy-product-card
                          :product="product"
                          :showWishlist="true"
                          :context="context"
                          :global_config="global_config"
                        ></fy-product-card> 
                      </div>
                    </div>
                  </div>
                  <div class="div2">
                    <div
                      class="glide__bullets" data-glide-el="controls[nav]">
                      <button
                        class="glide__bullet" :data-glide-dir="'=' + entry" v-for="(entry, index) in glidePaginate(products.length, getSectionValue(settings,'item_count'))" :key="index">
                      </button>
                    </div>
                  </div>
                  <div
                    class="arrows" 
                    v-if="products.length > getSectionValue(settings,'item_count')">
                    <section>
                      <div class="prev-btn btn-nav-gallery" ref="prevArrow" @click="prevSlide">
                        <div class="icon">
                          <svg-wrapper :svg_src="'nav-arrow'"></svg-wrapper>
                        </div>
                      </div>
                      <div class="next-btn btn-nav-gallery" ref="nextArrow" @click="nextSlide">
                        <div class="icon icon-next">
                          <svg-wrapper :svg_src="'nav-arrow'"></svg-wrapper>
                        </div>
                      </div>
                    </section>
                  </div>
                </div>
              </div>
            </template>
         
             <fdk-link :link="getSectionValue(settings,'button_link')">
              <sm-button
                :backgroundcolortype="'secondary'"
                :colortype="'primary'"
                :bordertype="'primary'"
                :padding="'primary'"
                :global_config="global_config"
                v-if="getSectionValue(settings,'button_text')"
              >{{ getSectionValue(settings,'button_text') }}</sm-button>
            </fdk-link>
          </div>
        </div>
      </div>
    </div>
  </template>
  <!-- #region  -->
  
  <settings>
  {
      "name": "col_ayush",
      "label": "Image ",
      "props": [
          {
              "type": "text",
              "id": "title",
              "default": "",
              "label": "Heading"
          },
          {
            "id": "mobile_layout",
            "type": "select",
            "options": [
                {
                    "value": "style11",
                    "text": "Style 1"
                },
                {
                    "value": "style22",
                    "text": "Style 2"
                }
            ],
            "default": "style1",
            "label": "Mobile Layout",
            "info": "Alignment of content"
          },
          {
              "id": "desktop_layout",
              "type": "select",
              "options": [
                  {
                      "value": "style1",
                      "text": "Style 1"
                  },
                  {
                      "value": "style2",
                      "text": "Style 2"
                  }
              ],
              "default": "style1",
              "label": "Desktop Layout",
              "info": "Alignment of content"
          },
          {
            "id": "collection",
            "type": "collection",
            "default": "",
            "label": "Collection",
            "info": "Alignment of content"
          },
          {
            "type": "url",
            "id": "button_link",
            "default": "",
            "label": "Redirect Link"
          },
          {
              "type": "text",
              "id": "button_text",
              "default": "",
              "label": "Button Text"
          }
      ]
  }
  </settings>
  <!-- #endregion -->
  <style scoped lang="less">
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
        > div {
          flex: 0 0 100%;
        }
      }
      .pr-img {
        display: grid;
        flex-flow: wrap;
        grid-template-columns: repeat(auto-fill,minmax(22%, 1fr));
        grid-auto-rows: auto;
        grid-template-rows: 1fr;
        grid-gap: var(--gapTop) var(--gap);
        gap: 30px;
        .tab {
          display: none;
        }
        .mob {
          display: none;
        }
        @media @tablet {
          grid-template-columns: repeat(auto-fill,minmax(31%, 1fr)); 
          .full {
            display: none;
          } 
          .tab {
            display: flex;
          }  
          .mob {
            display: none;
          } 
        }
        @media @mobile {
          grid-template-columns: repeat(auto-fill,minmax(31%, 1fr)); 
          .full {
            display: none;
          } 
          .tab {
            display: none;
          }  
          .mob {
            display: flex;
          }      
        }
      }
      .ayush {
        display: none;
        @media @mobile {
          display: flex;
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
      position: absolute;
      display: flex;
      justify-content: flex-end;
      bottom: 0%;
      right: 0;
      margin: -40px 0 0 0;
      @media @tablet {
        display: none;
      }
      section {
        position: relative;
        width: 100%;
        margin: 0 auto;
        display: flex;
        padding: 0 20px;
        box-sizing: border-box;
      }
    }
    .prev-btn {
      margin-right: 22px;
    }
    .glide__bullets {
      position: relative;
      z-index: 2;
      margin-top: 40px;
      bottom: 15px;
      left: 50%;
      // display: inline-flex;
      align-items: center;
      list-style: none;
      transform: translateX(-50%);
      @media @mobile {
        margin-top: 20px;
      }
    }
    .glide__bullet {
      background-color: unset;
      border: 1px solid @color-black;
      box-shadow: unset;
      // width: 80px;
      // border-radius: 0px;
      // height: 2px;
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
      .glide__slide {
        margin-right: 30px;
        width: auto;
        // max-width: 218px;
      }
    }
    .div2 {
      display: grid;
      grid-template-columns: auto 110px;
      padding: 1% 3%;
    }
    .btn-nav-gallery {
      z-index: @layer;
      background-color: transparent;
      padding: unset;
      cursor: pointer;
      width: 50px;
      display: flex;
      justify-content: center;
      transition: transform 0.2s;
      &:hover {
        transform: scale(1.2);
      }
    }
    .next-btn {
      margin-left: auto;
    }
    .icon {
      display: inline-block;
      width: 45px;
      height: 45px;
      background-size: cover;
    }
    .icon-next {
      transform: rotate(180deg);
    }
    .hero__image {
      /deep/ .fy__img {
        width: 100%;
      }
    }
    // .image {
    //   width: 306px;
    //   height: 408px;
    // }
    
    .imagesize {
      width: 306px;
    }
  }
  </style>
  <script>
  import { detectMobileWidth, glidePaginate } from "../helper/utils";
  import { isBrowser, isNode } from "browser-or-node";
  import Glide from "@glidejs/glide";
  import "../../node_modules/@glidejs/glide/dist/css/glide.core.min.css";
  import "../../node_modules/@glidejs/glide/dist/css/glide.theme.min.css";
  import btn from "./../components/common/button.vue";
  import SvgWrapper from "./../components/common/svg-wrapper.vue";
  import { getSectionValue } from "../helper/utils";
  import fyProduct from "../global/components/fy-product-card.vue";
  import emergeImage from "../global/components/common/emerge-image.vue";
  export default {
    props: ["settings", "apiSDK", "global_config"],
    components: {
      "sm-button": btn,
      "svg-wrapper": SvgWrapper,
      "fy-product-card": fyProduct,
      "emerge-img": emergeImage,
    },
    watch: {
      settings: function(newVal, oldVal) {
        this.cleanupComponent();
        this.initializeComponent();
      },
      products: function(newVal, oldVal) {
        this.cleanupComponent();
        this.initializeComponent();
      }
    }, 
   
    mounted() {
      let option = {
        slug: this.getSectionValue(this.settings,'collection')
      };
      this.fetchData(option);
      console.log("texttt++", this.settings);
      this.initializeComponent()
    },
    data: function() {
      return {
        products: [],
        image: [],
        title: [],
        description: [],
        isMounted: false,
        glideOptions: {
          type: 'carousel',
          startAt: 0,
          gap: 30,
          focusAt: 0,
          perView: this.getSectionValue(this.settings,'item_count'),
          breakpoints: {
            1214: { 
              perView: 3
            },
            780: {
              perView: 2
            },
            480: {
              perView: 1.5
            }
          }
        },
        carouselHandle: null
      };
    },
    methods: {
      getSectionValue,
      fetchData(option) {
        this.$apiSDK.catalog.getCollectionItemsBySlug(option).then(data => {
          console.log("data", data);
          this.image = data.items[0];
          console.log("++++++++++++++++++++++++",this.image);
          this.products = data.items;
          console.log("object", this.products);
          console.log("object++++++", this.products[0]);
        });
      },
      getImageUrl(medias) {
        return medias.url
      },
      checkisBrowser() {
        return isBrowser
      },
      glidePaginate,
      prevSlide() {
        let item_count = this.getSectionValue(this.settings,'item_count');
        if (detectMobileWidth()) {
          if (this.carouselHandle.index - 1 >= 0) {
            this.carouselHandle.go(`=${this.carouselHandle.index - 1}`);
          }
        } else {
          if (this.carouselHandle.index - item_count >= 0) {
            this.carouselHandle.go(`=${this.carouselHandle.index - item_count}`)
          } else {
            this.carouselHandle.go(`<<`);
          }
        }
      },
      nextSlide() {
        let item_count = this.getSectionValue(this.settings,'item_count');
        if (detectMobileWidth()) {
          if (this.carouselHandle.index + 1 >= this.products.length - 1) {
            this.carouselHandle.go(`=${this.carouselHandle.index + 1}`);
          }
        } else {
          if (
            this.carouselHandle.index + item_count <
            this.products.length)
            {
            this.carouselHandle.go(`=${this.carouselHandle.index + item_count}`);
          } else {
            this.carouselHandle.go(`>>`);
          }
        }
      },
      initCarousel() {
        if (
          isNode ||
          this.getSectionValue(this.settings,'desktop_layout') !== 'style2' || this.carouselHandle) {
          return;
        }
        if (!this.$refs.glide) {
          setTimeout(() => {
            this.initCarousel()
          }, 1000);
          return;
        }
        this.$nextTick(() => {
          try {
            if (window.screen.width > 480 && window.screen.width <= 768) {
              this.glideOptions.gap = 40;
            } else if (window.screen.width <= 480) {
              this.glideOptions.gap = 12;
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
              let currentDot = this.carouselHandle ? document.querySelectorAll(`.${glideClass} [data-glide-dir='=${this.carouselHandle.index}']`): null;
              if (currentDot && currentDot.length > 0) {
                currentDot[0].classList.add('glide__bullet--active');
              }
            })
            this.carouselHandle.mount()
          } catch (ex) {}
        })
      },
      initializeComponent() {
        this.isMounted = true;
        if (window.screen.width > 600 && window.screen.width <= 1024) {
          this.settings.props.item_count.value = 3;
        } else if (window.screen.width > 480 && window.screen.width <= 600) {
          this.settings.props.item_count.value = 2;
        } else if (window.screen.width <= 480) {
          this.settings.props.item_count.value = 1;
        }
        this.glideOptions.perView = this.settings.props.item_count.value;
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
    }
  };
  </script>