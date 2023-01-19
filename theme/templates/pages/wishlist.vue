<template>
  <div class="wl-cont my_wl_cont" :style="global_config ? 'color:' + global_config.props.text_body_color : ''">
    <div v-if="context.favourites && context.favourites.loading">
      <fdk-loader></fdk-loader>
    </div>
    <template v-if="
      context &&
      context.favourites &&
      context.favourites.items &&
      context.favourites.items.length
    ">
      <div class="">
        <h2 class="heading fontHead wl_title">
          Wishlist
        </h2>
        <div>
          <fdk-infinite-favourites>
            <template slot-scope="infiniteLoaderData">
              <div class="grid-wrapper">
                <div class="group-cards">
                  <div v-for="(product, index) in context.favourites.items" :key="`p-wl-${index}`">
                    <fdk-link :link="redirectPdp(product)" class="wl-link">
                      <fy-product-card :showWishlist="true" :isWishListPage="true" :product="product"
                        :global_config="global_config" />
                    </fdk-link>
                  </div>
                  <fdk-loader id="loader" v-if="infiniteLoaderData.hasNext"></fdk-loader>
                </div>

              </div>

            </template>
          </fdk-infinite-favourites>
        </div>
      </div>
    </template>
    <div v-else-if="context.favourites && !context.favourites.loading && !context.favourites.items.length">
      <!-- <fdk-empty-state title="Your Wishlist is empty." /> -->
      <div class="main_container">
        <div class="wl_title fontHead">
          Wishlist
        </div>
        <!-- <div class="fontSubHead"></div> -->
        <div class="sub_container">
          <div class="content">
            <div class="fontHead">
              You do not have any product added to wishlist
            </div>
            <div class="fontSubHead">
              Add products to wishilst
            </div>
            <div class="contShopBtn">
              <a href="/products">CONTINUE SHOPPING</a>
            </div>

          </div>

        </div>
      </div>
    </div>
  </div>
</template>
<style lang="less" scoped>
.wl-cont {
  // min-height: 600px;
  background: @White;

  // h2.heading {
  //   padding: 30px 0 0 20px;
  //   font-size: 30px;
  //   font-weight: 700;
  //   text-transform: uppercase;
  //   margin-bottom: 30px;
  //   text-align: left;
  // }

  .wl-link {
    -webkit-tap-highlight-color: transparent;
  }

  .grid-wrapper {
    margin: 24px 0px 0px 0px;
  }

  .group-cards {
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: 1fr;
    grid-gap: 2em;
  }

  @media screen and (max-width: 768px) {
    .group-cards {
      grid-template-columns: repeat(2,1fr);
      grid-gap: 0.5em;
    }
  }
}

.my_wl_cont {

  padding: 0px 72px;

  @media screen and (max-width: 768px) {
    padding: 0px 32px;

  }

  @media screen and (max-width: 480px) {
    padding: 0px 16px;

  }
}


.fontHead {
  //styleName: desktop/H3 - 28px Marcellus;
  font-family: Marcellus;
  font-size: 28px;
  font-weight: 400;
  line-height: 32px;
  letter-spacing: -0.02em;

  // text-align: center;
  @media screen and (max-width: 768px) {
    //styleName: Mobile/H3 - 24 px Marcellus;
    font-family: Marcellus;
    font-size: 24px;
    font-weight: 400;
    line-height: 28px;
    letter-spacing: -0.02em;

  }

}

.fontSubHead {
  //styleName: desktop/B1 - 16 px;
  font-family: Inter;
  font-size: 16px;
  font-weight: 400;
  line-height: 22px;
  letter-spacing: -0.02em;
  // text-align: center;

  @media screen and (max-width: 768px) {
    font-size: 14px;
  }
}

.wl_title {
  margin: 24px 0px;
}

.sub_container {
  height: 568px;
  text-align: center;
  background: rgba(241, 235, 229, 1);

  @media screen and (max-width: 768px) {
    height: 488px; //tm
  }

}

.contShopBtn {
  margin-top: 32px; //dtm
  width: 100%;
  display: inline-block;
  padding: 14px 0px; //dtm
  border: 1px solid rgba(38, 32, 26, 1);
  // color: var(--primaryColor);
  color: white;
  background: rgba(38, 32, 26, 1);
  text-align: center;
  //styleName: desktop/Button - 14 px;
  font-family: Inter;
  font-size: 14px;
  font-weight: 500;
  line-height: 20px;
  letter-spacing: -0.02em;

  @media screen and (max-width: 768px) {
    font-size: 12px;
  }

}

.content {
  width: 351px;
  padding-top: 194px;

  @media screen and (max-width: 768px) {
    width: 240px;
    padding-top: 151px;
  }

  @media screen and (max-width: 240px) {
    width: 240px;
    padding-top: 151px;
  }
}

.base-page-container {
   max-width: 1440px;
}

// ::v-deep .base-page-container {
//    max-width: 1440px;
// }
</style>
<script>
import productCard from "./../../global/components/fy-product-card.vue";
import loader from "./../../templates/components/loader.vue";

export default {
  name: "wishlist",
  components: {
    loader: loader,
    "fy-product-card": productCard,
  },
  methods: {
    redirectPdp(product) {
      if (product.sellable) {
        return `/product/${product.slug}`;
      }
      return;
    }
  },
};
</script>
