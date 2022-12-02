<template>
    <section class="d-hero-itb full-width-section" :class='["layout-" + settings.props.style_layout.value]'>
        <div class="d-hero-itb__content" :class='["mirror-" + settings.props.mirror_layout.value]'>
            <div class="d-hero-itb__content--sub">
                {{ settings.props.heading.value }}
            </div>
            <div class="d-hero-itb__content--main">
                <p>{{ settings.props.text.value }}</p>
            </div>
            <div class="heroBtn">
                <fdk-link :link="settings.props.button_link.value">
                    <sm-button :backgroundcolortype="'primary'" :colortype="'primary'" :bordertype="'primary'"
                        :padding="'primary'" :global_config="global_config" v-if="settings.props.button_text.value">
                        {{ settings.props.button_text.value }}
                    </sm-button>
                </fdk-link>
            </div>

        </div>
        <div :class='["image1-section",]' v-if="settings.props.image1.value">
            <img :src="settings.props.image1.value" />
        </div>

        <div class="newDiv" :class='["newDiv_mirror_" + settings.props.mirror_layout.value]'
            v-if="settings.props.image2.value && settings.props.style_layout.value == 'style_1'">
            <div class="image2-section" :class='["mirror-" + settings.props.mirror_layout.value]'>
                <img :src="settings.props.image2.value" />
            </div>
            <div class="text2">
                {{ settings.props.text2.value }}
            </div>
        </div>

    </section>
</template>  
<settings>
  {
    "name": "d-hero-itb",
    "label": "d-hero-itb",
    "props": [
        {
        "type": "select",
        "id": "style_layout",
        "options": [
            {
                "value": "style_1",
                "text": "Style 1"
            },
            {
                "value": "style_2",
                "text": "Style 2"
            },
            {
                
                "value": "style_3",
                "text": "Style 3"
            }
        ],
        "default": "style_3",
        "label": "Layout"
      },
      {
        "type": "select",
        "id": "mirror_layout",
        "options": [
            {
                "value": "on",
                "text": "On"
            },
            {
                "value": "off",
                "text": "Off"
            }
        ],
        "default": "on",
        "label": "Mirror Layout"
      },
      {
        "type": "text",
        "id": "heading",
        "default": "The Season Collection",
        "label": "Heading"
      },
      {
        "type": "text",
        "id": "text",
        "default": "Style solutions that are both flattering and functional for every occasion, whether it is on-duty or off-duty.",
        "label": "Short Description"
      },
      {
            "type": "text",
            "id": "button_text",
            "default": "Shop Now",
            "label": "Button Text"
      },
      
      {
            "type": "url",
            "id": "button_link",
            "default": "",
            "label": "Button Link"
      },
      {
        "type": "text",
        "id": "text2",
        "default": "Versatility and craftsmanship dominate this piece. Made from Vastrakala's classic 100% corduroy cotton. With Bedford corduroy, you get the look of corduroy without the nap. To keep all your belongings safe, this coat has five generously sized pockets.",
        "label": "Description"
      },
      
      {
        "type": "image_picker",
        "id": "image1",
        "default": "",
        "label": "Image 1"
      },
      {
        "type": "image_picker",
        "id": "image2",
        "default": "",
        "label": "Image 2"
      }
      
    ]
  }
  </settings>
  <!-- #endregion -->
<style lang="less" scoped>
.d-hero-itb {
    padding-bottom: 40px;
    padding-top: 40px;
    padding-right: 72px;
    padding-left: 72px;
    box-sizing: border-box;

    @media screen and (max-width: 768px) {
        padding-bottom: 32px;
        padding-top: 32px;
        padding-right: 0px;
        padding-left: 0px;
    }

    @media screen and (max-width: 480px) {
        padding-bottom: 16px;
        padding-top: 16px;
        padding-right: 0px;
        padding-left: 0px;

    }
}

.image1-section {
    @media screen and (max-width: 480px) {}
}

.heroBtn {
    margin-bottom: 40px;
    margin-top: 30px;

}

.d-hero-itb>.d-hero-itb__content {
    display: flex;
    flex-direction: column;

    @media screen and (max-width: 480px) {
        padding-left: 16px;
        padding-right: 16px;
    }
}

.d-hero-itb>.d-hero-itb__content>.d-hero-itb__content--sub {
    font-family: Marcellus;
    font-weight: 400;
    font-size: 80px;
    line-height: 90px;

    @media screen and (max-width: 768px) {
        font-size: 40px;
        line-height: 44px;
    }

    @media screen and (max-width: 480px) {
        font-size: 40px;
        line-height: 44px;
    }
}

.d-hero-itb>.d-hero-itb__content>.d-hero-itb__content--main {
    font-family: inter;
    padding-top: 8px;
    font-size: 16px;
    font-weight: 400;
    line-height: 22px;

    @media screen and (max-width: 768px) {
        font-size: 14px;
        line-height: 20px;
    }

    @media screen and (max-width: 480px) {
        font-size: 14px;
        line-height: 20px;
    }
}

.d-hero-itb>.mirror-off {
    order: 0;

    @media screen and (max-width: 480px) {
        order: 1;
    }
}

.d-hero-itb>.mirror-on {
    order: 1;
}

//------------------------S3 Only------------------------
.layout-style_3 {
    align-items: center;
    text-align: center;
    flex-direction: column;
    flex-wrap: wrap;
    display: flex;
}


.layout-style_3>.d-hero-itb__content {
    padding-top: 40px;
    //width: 932px;
    display: inline-flex;

    @media screen and (max-width: 768px) {
        width: 464px;
        padding-top: 32px;
    }

    @media screen and (max-width: 480px) {
        width: 288px;
        padding-top: 16px;
        padding-left: 32px; //fynd=16px
        text-align: left;
        display: flex;
    }
}

.layout-style_3>.mirror-on {
    order: 1;
}

.layout-style_3>.mirror-off {
    order: 0;
}


.layout-style_3>.image1-section {
    box-sizing: border-box;
    display: inline-block;
    box-sizing: border-box;
    padding-top: 40px;
    padding-bottom: 16px;
}

.layout-style_3>.image1-section>img {
    max-width: 100%;
    width: 1296px;
    height: 729px;
    object-fit: cover;

    @media screen and (max-width: 768px) {
        width: full;
        height: 418px;
    }

    @media screen and (max-width: 480px) {
        width: full;
        height: 426px;
    }

}



//------------------------S2 only--------------------------


//-------------------------S1S2--------------------------
.layout-style_2,
.layout-style_1 {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;

}

.layout-style_2>.d-hero-itb__content,
.layout-style_1>.d-hero-itb__content {
    padding-top: 176px;
    width: 456px;
    display: inline-block;
    text-align: left;

    @media screen and (max-width: 768px) {
        width: 318px;
        padding-top: 114px;
    }

    @media screen and (max-width: 480px) {
        width: 288px;
        padding-top: 0px;
        padding-left: 16px;
    }
}

.layout-style_2>.mirror-off,
.layout-style_1>.mirror-off {
    padding-right: 200px;

    @media screen and (max-width: 768px) {
        padding-right: 32px;
        padding-left: 32px;
    }

    @media screen and (max-width: 480px) {
        padding-right: 0px;


    }
}

.layout-style_2>.mirror-on,
.layout-style_1>.mirror-on {
    padding-left: 128px;

    @media screen and (max-width: 768px) {
        padding-left: 40px;
    }

    @media screen and (max-width: 480px) {}
}

.layout-style_2>.image1-section,
.layout-style_1>.image1-section {
    box-sizing: border-box;
    display: inline-block;
    box-sizing: border-box;
}

.layout-style_2>.image1-section>img,
.layout-style_1>.image1-section>img {
    max-width: 100%;
    //aspect-ratio: 3/4;
    width: 640px;  
    height: 853px;
    object-fit: cover;

    @media screen and (max-width: 768px) {
        width: 360px;
        height: 480px;
    }

    @media screen and (max-width: 480px) {
        width: 296px;
        height: 394px;
    }

}

//------------------------S1 only--------------------------

.newDiv {
    display: flex;
    flex-direction: row;
    order: 2;

    @media screen and (max-width: 480px) {
        display: flex;
        flex-direction: column-reverse;
        flex-wrap: wrap;
    }
}

.newDiv>.image2-section {
    display: flex;
    flex-direction: row;
    order: 2;
    box-sizing: border-box;
    margin-top: -149px; //by fynd

    @media screen and (max-width: 768px) {
        margin-top: 24px;
    }

    @media screen and (max-width: 480px) {}
}

.newDiv>.image2-section>img {
    max-width: 100%;
    width: 444px;
    height: 592px;
    object-fit: cover;

    @media screen and (max-width: 768px) {
        width: 234px;
        height: 312px;
    }

    @media screen and (max-width: 480px) {
        width: 234px;
        height: 312px;
    }
}

.newDiv>.mirror-off {

    order: 0;

    @media screen and (max-width: 768px) {
        padding-left: 32px;
    }

    @media screen and (max-width: 480px) {
        padding-left: 0px;
        order: 1;

    }
}

.newDiv>.mirror-on {
    padding-left: 220px;
    order: 1;

    @media screen and (max-width: 768px) {
        padding-left: 40px;
    }

    @media screen and (max-width: 480px) {
        padding-left: 0px;
    }
}

.newDiv>.text2 {
    padding-left: 103px;
    padding-top: 71px;
    text-align: left;
    width: 546px;
    order: 0;
    font-family: inter;
    font-size: 16px;
    font-weight: 400;
    line-height: 22px;

    @media screen and (max-width: 768px) {
        font-size: 14px;
        line-height: 20px;
        width: 322px;
        padding-top: 24px;
        padding-left: 40px; //mirror off =40px , mir-on = 92px
    }

    @media screen and (max-width: 480px) {
        width: 234px;
        font-size: 14px;
        line-height: 20px;
        padding-left: 0px;
    }


}

.newDiv_mirror_on {
    @media screen and (max-width: 768px) {

        padding-left: 52px;
    }

    @media screen and (max-width: 480px) {

        padding-left: 70px;

    }
}

.newDiv_mirror_off {

    @media screen and (max-width: 480px) {

        padding-left: 16px;

    }
}







//------------------------------------------------------
</style>
  
<script>
import btn from "./../components/common/button.vue";


export default {
    data() {
        return {

        };
    },

    components: {
        "sm-button": btn,
    },
    props: ["settings", "global_config"],
    watch: {
        settings: function (newVal, oldVal) { },
    },
    directives: {},
    mounted() { },
    beforeDestroy() {

    },
};
</script>
  