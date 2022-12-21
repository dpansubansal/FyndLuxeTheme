<template>
    <section class="d-hero-itb full-width-section" :class='["layout-" + settings.props.style_layout.value]'>
        <div class="primaryDiv">
            <div class="d-hero-itb__content" :class='["mirror-" + settings.props.mirror_layout.value]'>
                <div class="d-hero-itb__content--sub">
                    {{ settings.props.heading.value }}
                    <div class="whites100"></div>
                </div>
                <div class="d-hero-itb__content--main fadeIn">
                    <p>{{ settings.props.text.value }}</p>
                </div>
                <div class="heroBtn fadeIn">
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
                <div class="whites50"></div>
            </div>
        </div>

        <div class="newDiv" :class='["newDiv_mirror_" + settings.props.mirror_layout.value]'
            v-if="settings.props.image2.value && settings.props.style_layout.value == 'style_1'">
            <div class="image2-section" :class='["mirror-" + settings.props.mirror_layout.value]'>
                <img :src="settings.props.image2.value" />
                <div class="whites50"></div>
            </div>
            <div class="text2 fadeIn">
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
        "label": "Layout",
        "info":"Three different type layout for desktop, tablet and mobile view"
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
        "label": "Heading",
        "info":"Heading text of the section "
      },
      {
        "type": "text",
        "id": "text",
        "default": "Style solutions that are both flattering and functional for every occasion, whether it is on-duty or off-duty.",
        "label": "Short Description",
        "info":" Shot description text below the heading on UI"
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

.d-hero-itb>.primaryDiv>.d-hero-itb__content {
    display: flex;
    flex-direction: column;

    @media screen and (max-width: 480px) {
        padding-left: 16px;
        padding-right: 16px;
    }
}

.d-hero-itb>.primaryDiv>.d-hero-itb__content>.d-hero-itb__content--sub {
    font-family: Marcellus;
    font-weight: 400;
    font-size: 80px;
    //font-size: 400%;
    //line-height: 90px;
    line-height: 100%;

    @media screen and (max-width: 1140px) {
        font-size: 40px;
        line-height: 44px;
    }

    @media screen and (max-width: 768px) {
        font-size: 40px;
        line-height: 44px;
    }

    @media screen and (max-width: 480px) {
        font-size: 40px;
        line-height: 44px;
    }
}

.d-hero-itb>.primaryDiv>.d-hero-itb__content>.d-hero-itb__content--main {
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





.d-hero-itb>.primaryDiv>.mirror-off {
    order: 0;

    @media screen and (max-width: 480px) {
        order: 1;
    }
}

.d-hero-itb>.primaryDiv>.mirror-on {
    order: 1;
}

//------------------------S2 only--------------------------


//-------------------------S1S2--------------------------
.layout-style_2,
.layout-style_1 {
    display: flex;
    flex-direction: column;

    @media screen and (max-width: 480px) {
        flex-wrap: wrap;
    }


}

.layout-style_1>.primaryDiv,
.layout-style_2>.primaryDiv {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;

    @media screen and (max-width: 480px) {
        flex-direction: column;
    }
}

.layout-style_2>.primaryDiv>.d-hero-itb__content,
.layout-style_1>.primaryDiv>.d-hero-itb__content {
    //padding-top: 176px;
    //width: 456px;
    margin-top: 10%;
    flex: 50%;
    text-align: left;



    @media screen and (max-width: 768px) {
        width: 318px;
        //padding-top: 114px;
    }

    @media screen and (max-width: 480px) {
        width: 288px;
        padding-top: 0px;
        padding-left: 16px;
    }
}

.layout-style_2>.primaryDiv>.mirror-off,
.layout-style_1>.primaryDiv>.mirror-off {
    //padding-right: 200px;
    padding-right: 3%;

    @media screen and (max-width: 768px) {
        // padding-right: 32px;
        // padding-left: 32px;
        padding-left: 3%;
    }

    @media screen and (max-width: 480px) {
        padding-right: 0px;


    }
}



.layout-style_2>.primaryDiv>.mirror-on,
.layout-style_1>.primaryDiv>.mirror-on {
    //padding-left: 128px;
    padding-left: 5%;

    @media screen and (max-width: 768px) {
        //padding-left: 40px;
    }

    @media screen and (max-width: 480px) {}
}

.layout-style_2>.primaryDiv>.d-hero-itb__content>.d-hero-itb__content--main,
.layout-style_1>.primaryDiv>.d-hero-itb__content>.d-hero-itb__content--main {
    padding-right: 30%;

}

.layout-style_2>.primaryDiv>.image1-section,
.layout-style_1>.primaryDiv>.image1-section {

    flex: 50%;

    @media screen and (max-width: 480px) {
        width: 100%
    }
}

.layout-style_2>.primaryDiv>.image1-section>img,
.layout-style_1>.primaryDiv>.image1-section>img {
    //max-width: 100%;
    //aspect-ratio: 3/4;
    //width: 640px;  
    //height: 853px;
    //min-height: 380px;
    width: 100%;
    height: auto;
    aspect-ratio: 3/4;
    object-fit: cover;

    @media screen and (max-width: 768px) {
        //width: 360px;
        // height: 480px;
        //width: 100%;
        //height: auto;
    }

    @media screen and (max-width: 480px) {
        //width: 296px;
        //height: 394px;
        width: 100%;
        height: auto;
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
    margin-top: -10%;
    //margin-top: -149px; //by fynd

    @media screen and (max-width: 768px) {
        margin-top: 24px;
    }

    @media screen and (max-width: 480px) {}
}

.newDiv>.image2-section>img {
    //max-width: 100%;
    //width: 444px;
    //height: 592px;
    width: 100%;
    height: auto;
    max-width: 1200px;
    aspect-ratio: 3/4;
    object-fit: cover;

    @media screen and (max-width: 768px) {
        width: 234px;
        height: 312px;
    }

    @media screen and (max-width: 480px) {
        //width: 234px;
        width: 100%;

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
    //padding-left: 220px;
    order: 1;

    @media screen and (max-width: 768px) {
        padding-left: 40px;
    }

    @media screen and (max-width: 480px) {
        padding-left: 0px;
    }
}

.newDiv>.text2 {
    //padding-left: 103px;
    padding-top: 71px;
    padding-right: 5%;
    padding-left: 5%;
    text-align: left;
    //width: 546px;
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
        //width: 234px;
        padding: 5%;
        width: 100%;
        font-size: 14px;
        line-height: 20px;
        padding-left: 0px;
    }


}

.newDiv_mirror_on {
    @media screen and (max-width: 768px) {

        padding-left: 1%;
    }

    @media screen and (max-width: 480px) {

        //padding-left: 70px;
        padding-left: 0px;

    }
}

.newDiv_mirror_off {

    @media screen and (max-width: 480px) {

        padding-left: 16px;

    }
}


//------------------------S3 Only------------------------
.layout-style_3 {
    align-items: center;
    text-align: center;
    flex-direction: column;
    flex-wrap: wrap;
    display: flex;
}

.layout-style_3>.primaryDiv {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.layout-style_3>.primaryDiv>.d-hero-itb__content {
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

.layout-style_3>.primaryDiv>.mirror-on {
    order: 1;
}

.layout-style_3>.primaryDiv>.mirror-off {
    order: 0;
}


.layout-style_3>.primaryDiv>.image1-section {
    box-sizing: border-box;
    display: inline-block;
    box-sizing: border-box;
    padding-top: 40px;
    padding-bottom: 16px;
}

.layout-style_3>.primaryDiv>.image1-section>img {
    max-width: 100%;
    width: 1296px;
    max-height: 729px;
    aspect-ratio: 4/3;
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

//-------------------------Animation Ready-----------------------------

.image1-section,.d-hero-itb__content--sub,.image2-section{
      position: relative;
    }
    .fadeIn{
      animation-name: fadeIn;
    animation-duration: 4s;

    }
    
    .whites50{
      position: absolute;
      top:0px;
      left:0px;
      width: 100%;
      height: 100%;
     background-color: white;
     animation-name: example50;
    animation-duration: 1.2s;
    animation-delay: 1s;
    animation-direction:reverse;
    animation-fill-mode: forwards;
    animation-timing-function: ease-out;

    }
    .whites100{
      position: absolute;
      top:0px;
      left:0px;
      width: 100%;
      height: 100%;
     background-color: white;
     animation-name: example100;
    animation-duration: 1s;
    animation-direction:reverse;
    animation-fill-mode: forwards;

    }
    @keyframes fadeIn {
      0% { opacity: 0; }
      100% { opacity: 1; }
    }

    @keyframes example50 {
      0%   {height:0%;}
      
      100% {height:50%;}
    }
    @keyframes example100 {
      0%   {height:0%;}
      
      100% {height:100%;}
    }
    



//------------------------------------------------------

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
  