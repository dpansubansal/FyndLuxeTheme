<template>
  <div class="section-margin-db">
    <!-- <PageLoader /> -->
    <div class="collections__template xyz"
      :style="global_config ? 'color:' + global_config.props.text_body_color : ''">
      <template v-if="context.collections && context.collections.items && context.collections.items.length > 0">
        <div class="card-container">
          <div class="top-items">
            <div class="title-block">
              <div class="section-heading fontHead" :style="'color:' + global_config.props.text_heading_link_color">
                Collection <!-- {{ page_config.props.title }} --><!-- {{ context.collections.items }} -->
              </div>
            </div>
            <div class="sub-title-block">
              <div class="fontSub">
                Browse through stylish women’s topwear that is offered by popular brands, such as Jockey, Darzi, Ann
                Springs, and more. Browse through stylish women’s topwear that is offered by popular brands, such as
                Jockey, Darzi, Ann Springs, and more.Browse through stylish women’s topwear that is offered by popular
                brands, such as Jockey, Darzi, Ann Springs, and more.
              </div>
            </div>
            <!-- <fdk-infinite-collections class="plp-container" :handleinfinite=true>
            <template slot-scope="collectionListing">
              <div class="product-container">
                <div class="grp_card_adv">
                  {{ printConsole(context.collections.items) }}
                  <div class="card_item_adv" v-for="card in context.collections.items" :key="card">
                    <fdk-link :action="card.action">
                      <div class="item_img">
                        <div class="card_img"><img :src="card.banners.portrait.url" /></div>
                      </div>
                      <div class="item_txt">{{ card.name }}</div>
                    </fdk-link>
                  </div>
                </div>
                <button v-if="context.collections.page.has_next" @click="collectionListing.loadmore">next</button>
                <fdk-loader id="loader" class="loader-center" v-if="context.collections.page.has_next"></fdk-loader>
              </div>
            </template>
          </fdk-infinite-collections> -->

            <fdk-infinite-collections>
              <template slot-scope="collectionListing">
                <fdk-infinite-scrolling :loadingData="loading" v-on:loadmore="collectionListing.loadmore">
                  <div class="grp_list_wrap_adv">
                    <div class="grp_card_adv">
                      <div class="card_item_adv" v-for="card in filterProducts8" :key="card">
                        <fdk-link :action="card.action">
                          <div class="item_img">
                            <div class="card_img"><img :src="card.banners.portrait.url" /></div>
                          </div>
                          <div class="item_txt">{{ card.name }}</div>
                        </fdk-link>
                      </div>
                    </div>
                    <banner-db :bnr_img1="getPageConfigById('image1')" :bnr_img2="getPageConfigById('image2')"
                      :bnr_head="getPageConfigById('bHead')" :bnr_subhead="getPageConfigById('bSubHead')"
                      :btn_txt="getPageConfigById('button_text')" :btn_link="getPageConfigById('button_link')" />
                    <div class="grp_card_adv">
                      <div class="card_item_adv" v-for="card in filterProducts8plus" :key="card">
                        <fdk-link :action="card.action">
                          <div class="item_img">
                            <div class="card_img"><img :src="card.banners.portrait.url" /></div>
                          </div>
                          <div class="item_txt">{{ card.name }}</div>
                        </fdk-link>
                      </div>
                    </div>
                  </div>
                </fdk-infinite-scrolling>
              </template>
            </fdk-infinite-collections>
            <fdk-loader v-if="!(context.collections.page.has_next === false)" id="loader"></fdk-loader>
          </div>
        </div>
      </template>
      <fdk-empty-state
        v-else-if="context.collections && context.collections.items && context.collections.items.length === 0 && isMounted"
        :title="'No Collections Found'"></fdk-empty-state>
      <back-to-top-db class="b2top" />
    </div>
  </div>
</template>
<!-- #region  -->

<settings>
{
    "props": [
        {
            "type": "text",
            "id": "title",
            "default": "",
            "label": "Title"
        },
        {
            "type": "range",
            "id": "items_per_row",
            "min": 3,
            "max": 8,
            "step": 1,
            "unit": "",
            "label": "Items per row",
            "default": 5,
            "info": "Maximum items allowed per row"
        },
        {
            "type": "image_picker",
            "id": "image1",
            "default": "",
            "label": "Image 1",
            "info": "Pls attach Image"
        },
        {
            "type": "image_picker",
            "id": "image2",
            "default": "",
            "label": "Image 2",
            "info": "Pls attach Image"
        },
        {
            "type": "text",
            "id": "bHead",
            "default": "Explore Our Outfits",
            "label": "Banner Heading"
        },
        {
            "type": "text",
            "id": "bSubHead",
            "default": "Curated list of our best outfit combinations designed by Vastrakala experts",
            "label": "Banner Subheading"
        },
        {
            "type": "text",
            "id": "button_text",
            "default": "Read article",
            "label": "Button Text"
       },
       {
            "type": "url",
            "id": "button_link",
            "default": "",
            "label": "Button Link"
       }
    ]
}
</settings>
<!-- #endregion -->
<script>
import groupList from "./../../global/components/group-list.vue";
import emergeImage from "./../../global/components/common/emerge-image.vue";
import placeholderItemsVue from "../../global/components/sections/placeholder-items.vue";
import bannerDB from "./../../global/components/plp/banner-db";
import backToTopDB from "./../../global/components/plp/back-to-top-db";
import PageLoader from "./../../global/components/plp/loader-db.vue";


export default {
  data() {
    return {
      collections: [],
      isLoading: false,
      isMounted: false,
    };
  },
  components: {
    "group-list": groupList,
    "emerge-image": emergeImage,
    "placeholder-items": placeholderItemsVue,
    "banner-db": bannerDB,
    "back-to-top-db": backToTopDB,
    "PageLoader": PageLoader,
  },
  watch: {
    settings: function (newVal, oldVal) { },
  },
  mounted() {
    this.isMounted = true
  },
  methods: {
    getPageConfigById(id) {
      return this.page_config?.props?.[id] || "";
    },
    printConsole(dataa) {
      console.log(dataa);
    },
  },
  computed: {
    filterProducts8: function () {
      return this.context.collections.items.filter((item, index) => index < 8)
    },
    filterProducts8plus: function () {
      return this.context.collections.items.filter((item, index) => index >= 8)
    },
  }
};
</script>

<style lang="less" scoped>
/deep/ .infi-loader {
  .container {
    background-color: transparent;
  }
}

::-webkit-scrollbar {
  display: none;
}

.collections {

  // &__template {
  //   // .section-heading {
  //   //   font-size: 18px;
  //   //   text-align: left;
  //   //   color: #41434c;
  //   //   margin-bottom: 6px;
  //   //   @media @mobile {
  //   //     font-size: 14px;
  //   //     margin-bottom: 6px;
  //   //     margin-left: 9px;
  //   //   }
  //   // }
  // }

  //&__template {
  //.section-main-container{
  //max-width: 1440px;
  //}
  //}

  &__content {
    top: 92%;
    position: absolute;
    display: flex;
    width: 100%;
    left: 50%;
    transform: translate(-50%, -50%);
    /* flex-direction: column; */
    /* justify-content: center; */
    /* align-items: center; */
    /* opacity: 0; */
    transition: all 0.5s;
    background: transparent linear-gradient(180deg, transparent, #000) 0 0 no-repeat padding-box;
    color: #ffffff;
    border-radius: 8px;
  }
}

.card-container {
  margin: 0;
  position: relative;
}

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
  //.margin-0-auto();

  >div {
    flex: 0 0 100%;
  }
}


.item {
  padding-right: 20px;
  box-sizing: border-box;
}

.grp_card_adv {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 1fr;
  grid-template-rows: 1fr;
  grid-gap: 48px 24px;

  @media screen and (max-width: 768px) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media screen and (max-width: 480px) {
    grid-gap: 32px 12px;
  }
}

.card_img>img {
  width: 100%;
  aspect-ratio: 0.75;
}

.item_txt {
  margin-top: 16px; //dtm
}

.fontSub {
  font-family: Inter;
  font-size: 14px;
  font-weight: 400;
  line-height: 20px;
  letter-spacing: -0.02em;
  text-align: left;
  margin-bottom: 24px;

  @media screen and (max-width: 480px) {
    //styleName: Mobile/B2 - 12px;
    font-family: Inter;
    font-size: 12px;
    font-weight: 400;
    line-height: 20px;
    letter-spacing: -0.02em;
    text-align: left;
    margin-bottom: 16px;
  }


}

.fontHead {
  //styleName: desktop/H2 - 32px Marcellus;
  font-family: Marcellus;
  font-size: 32px;
  font-weight: 400;
  line-height: 36px;
  letter-spacing: -0.02em;
  text-align: left;
  margin-bottom: 8px;

  @media screen and (max-width: 480px) {
    //styleName: Mobile/H2 - 28 px Marcellus;
    font-family: Marcellus;
    font-size: 28px;
    font-weight: 400;
    line-height: 32px;
    letter-spacing: -0.02em;
    text-align: left;
  }
}

.item_txt {
  @media screen and (max-width: 480px) {
    //styleName: Mobile/Sub H6- 14px Medium;
    font-family: Inter;
    font-size: 14px;
    font-weight: 500;
    line-height: 16px;
    letter-spacing: -0.02em;
    text-align: left;

  }
}
</style>
