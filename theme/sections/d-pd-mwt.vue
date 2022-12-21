<template>
    <section
        :class='["d-pd-mwt", "full-width-section", "layout-" + settings.props.style_layout.value, "mirror-" + settings.props.mirror_layout.value]'>
        <div :class='["image-section"]' v-if="settings.props.image.value">
            <img :src="settings.props.image.value" />
        </div>
        <div :class='["d-pd-mwt__content",]'>
            <div class="d-pd-mwt__content--sub">
                {{ settings.props.heading.value }}
            </div>
            <div class="d-pd-mwt__content--main">
                {{ settings.props.text.value }}
            </div>

        </div>
    </section>
</template>
  <!-- #region  -->
  
<settings>
  {
    "name": "d_pd_mwt",
    "label": "Dipanshu PD Section",
    "props": [
     {
        "type": "select",
        "id": "style_layout",
        "options": [
            {
                "value": "style1",
                "text": "Style 1"
            },
            {
                "value": "style2",
                "text": "Style 2"
            },
            {
                "value": "style3",
                "text": "Style 3"
            }
        ],
        "default": "style1",
        "label": "Style Layout"
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
        "default": "Designed as companion pieces to share with friends and family, collection serves dual purpose.",
        "label": "Heading"
      },
      {
        "type": "text",
        "id": "text",
        "default": "Vastrakala is a modern design studio committed to producing thoughtful, high-quality items for everyday use. We have always appreciated the attention to detail put into traditional and casual clothing, as well as the notion that the wearer is the only one who can properly appreciate the uniqueness of the item they are donning. Clothing, whether for men or women, may have clean, timeless lines with a nod to nostalgia while maintaining a feeling of uniqueness and charm.",
        "label": "Text"
      },
      {
        "type": "image_picker",
        "id": "image",
        "default": "",
        "label": "Image"
      }
    ]
  }
  </settings>
  <!-- #endregion -->
<style lang="less" scoped>
.d-pd-mwt {
    display: flex;
    justify-content: space-around;
    font-size: 16px;
    font-weight: 300;
    padding: 16px 40px;
    box-sizing: border-box;


    @media @large-1280 {
        padding-left: 0px;
        padding-right: 0px;
        flex-direction: column;
    }

    .image-section {
        flex: 0 0 50%;
        box-sizing: border-box;

        img {
            max-width: 100%;
        }
    }


    &__content {
        // flex: 0 0 50%;
        padding-left: 2%;
        padding-right: 2%;
        display: flex;
        order: 0;
        flex-direction: column;
        text-align: left;
        line-height: 35px;
        box-sizing: border-box;

        @media @mobile {
            padding: 25px;
        }

        &.al-left {
            text-align: left;

            @media @large-1280 {
                text-align: center;
            }
        }

        &.al-center {
            text-align: center;
        }

        &.al-right {
            text-align: right;

            @media @large-1280 {
                text-align: center;
            }
        }

        &--main {
            padding: 10px;
            font-size: 15px;
            font-weight: 300;
            line-height: 31px;

            @media @mobile {
                font-size: 12px;
                line-height: 18px;
            }
        }

        &--sub {
            margin-top: 5px;
            padding: 10px;
            font-size: 30px;
            font-weight: 400;
            line-height: 31px;

            @media @mobile {
                font-size: 12px;
                line-height: 18px;
            }
        }
    }
}

.layout-style2>.image-section>img {
    max-width: 100%;
    height: 55%;
    width: 100%;
    object-fit: cover;
}

.mirror-on {
    flex-direction: row-reverse;

    @media @tablet {
        flex-direction: column;
    }

    @media @mobile {
        flex-direction: column;
    }
}

.mirror-off {
    flex-direction: row;

    @media @tablet {
        flex-direction: column;
    }

    @media @mobile {
        flex-direction: column;
    }
}

@media screen and (max-width: 1160px) {}
</style>
  
<script>

export default {
    data() {
        return {

        };
    },
    props: ["settings", "global_config"],
    computed: {
    },
    components: {

    },
    watch: {
        settings: function (newVal, oldVal) { },
    },
    directives: {},
    mounted() { },
    beforeDestroy() {

    },
};
</script>
  