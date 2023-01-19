<template>
  <div>
    <fdk-link :link="settings.props.button_link.value">
      <emerge-img
        v-if="settings.props.image.value"
        :src="settings.props.image.value"
        :sources="[]"
        class="hero__image"
      />
      <fdk-placeholder v-else type="banner-1" />
      <div class="overlay">
        <div class="overlay__content">
          <img
            v-if="settings.props.overlay_image.value"
            class="overlay__image"
            :src="settings.props.overlay_image.value"
          />
        </div>
      </div>
    </fdk-link>
  </div>
</template>
<!-- #region  -->

<settings>
{
    "name": "banner",
    "label": "Banner",
    "props": [
        {
            "id": "image",
            "type": "image_picker",
            "label": "Desktop Image",
            "default": ""
        },
        {
            "type": "image_picker",
            "id": "overlay_image",
            "default": "",
            "label": "Mobile Image",
            "info": "Overlay Image"
        },
        {
            "type": "url",
            "id": "button_link",
            "default": "",
            "label": "Redirect Link"
        }
    ]
}
</settings>
<!-- #endregion -->
<style scoped lang="less">
.hero__image {
  /deep/ .fy__img {
    width: 100%;
    @media @mobile{
      display: none;
    }
  }
}
.hero__image::before {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background: var(--bg-color);
  animation: b-ltr-before 1.5s cubic-bezier(0, 0, 0, 0) forwards;
  background-color: white;
}
.hero__image:nth-of-type(1)::before,
.hero__image:nth-of-type(1)::after {
    animation-delay: 0.5s;
}
@keyframes b-ltr-after {
    0% {
        transform: translateY(-100%)
    }
    100% {
        transform: translateY(101%)
    }
}
@keyframes b-ltr-before {
    0% {
        transform: translateY(0)
    }
    100% {
        transform: translateY(-200%)
    }
}
.overlay {
  position: absolute;
  top: 30%;
  left: 50%;
  width: 100%;
  transform: translate(-50%, -50%);
  // display: flex;
  &__image {
    display: none;
    max-width: 100%;
    margin-bottom: 10px;
    @media @mobile {
      display: flex;
      height: 400px;
    }
  }
}
.overlay::before {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background: var(--bg-color);
  animation: b-ltr-before 1.5s cubic-bezier(0, 0, 0, 0) forwards;
  background-color: white;
}
.overlay:nth-of-type(1)::before,
.overlay:nth-of-type(1)::after {
    animation-delay: 0.5s;
}
@keyframes b-ltr-after {
    0% {
        transform: translateY(-100%)
    }
    100% {
        transform: translateY(101%)
    }
}
@keyframes b-ltr-before {
    0% {
        transform: translateY(0)
    }
    100% {
        transform: translateY(-200%)
    }
}
</style>

<script>
import btn from "./../components/common/button.vue";
import emergeImage from "../global/components/common/emerge-image.vue";
export default {
  components: {
    "emerge-img": emergeImage
  },
  props: ["settings", "global_config"],
  watch: {
    settings: function(newVal, oldVal) {},
  },
  mounted() {},
  data: function() {
    return {
      // url: ""
    };
  },
};
</script>