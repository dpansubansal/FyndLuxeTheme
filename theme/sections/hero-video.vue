<template>
  <div class="section-wrapper full-width-section" :style="dynamicStyles" v-if="render">
    <!-- <div class="video-container" :class="getValueById('size')"> -->
    <div class="video-container">
      <video ref="mp4video" width="100%" :poster="getValueById('cover_url')" :autoplay="checkVideoAutoplay()"
        :muted="settings.props.mute.value" :loop="settings.props.loop.value" :controls="checkVideoControls() ? false : true" playsinline
        @pause="showOverlay = true" @ended="showOverlay = true" preload="auto" v-if="isMp4()">
        <source :src="settings.props.video_url.value" type="video/mp4" allowfullscreen />
      </video>
      <!-- <div class="yt-container" v-else-if="isYoutube()">
        <div class="yt-video" ref="ytVideo" :id="'yt-video-' + getYTVideoID(settings.props.video_url.value)"
          :data-videoid="getYTVideoID(settings.props.video_url.value)" :data-videometa="JSON.stringify(settings.props)"
          allowfullscreen></div>
      </div> -->
      <div id="video_overlay" ref="video_overlay" class="overlay animated fadeIn" v-show="showOverlay">
        <div v-if="
          settings.props.cover_url.value
        " class="overlay__image"
          :style="`background: #ccc url(${getValueById('cover_url')}) center center / cover no-repeat;`"></div>
        <!-- <div v-if="checkOverlaySize('container')" class="overlay__color"
          :style="`background-color:black; opacity: 0.6 `"></div> -->
        <div class="overlay__content center-center">
          <div class="overlay__color"
            :style="`background-color:black ; opacity:0.6`"></div>
          <div class="overlay__content--text">
            <div @click="playVideo" class="play-button">
              <svg-wrapper :svg_src="'play'"></svg-wrapper>
            </div>
            <div class="overlay__text" v-if="
              settings.props.heading.value || settings.props.description.value
            ">
              <h2 v-if="settings.props.heading.value" :style="`color:white;`">
                {{ settings.props.heading.value }}
              </h2>
              <p v-if="settings.props.description.value" :style="`color:white;`">
                <span>{{ settings.props.description.value }} </span>
              </p>
            </div>


          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<!-- #region  -->
<settings>
{
  "name": "hero_video",
  "label": "Hero Video",
  "props": [
    {
      "id": "video_url",
      "type": "text",
      "label": "Video link",
      "default": "",
      "info":"Supports MP4 Video & Youtube Video URL"
    },
    {
      "type": "checkbox",
      "id": "autoplay",
      "default": false,
      "label": "Autoplay",
      "info":"Check to enable autoplay (Video will be muted if autoplay is active)"
    },
    {
      "type": "checkbox",
      "id": "controls",
      "default": false,
      "label": " Hide Video Controls",
      "info":"Uncheck to enable video controls"
    },
    {
      "type": "checkbox",
      "id": "loop",
      "default": true,
      "label": " Play Video in Loop",
      "info":"Uncheck to stop play video in loop"
    },
    {
      "type": "checkbox",
      "id": "mute",
      "default": true,
      "label": "Mute Audio",
      "info":"Uncheck to unmute the video"
    },
   
    {
      "type": "text",
      "id": "heading",
      "default": "Watch Show Reel",
      "label": "Heading"
    },
   
    {
      "type": "text",
      "id": "description",
      "default": "Backed by one of Europe's largest natural beauty companies, MyGlamm collaborated with global experts and makeup artists to bring about exciting innovation in makeup to accomplish our single, focused goal make looking glamorous effortless!",
      "label": "Description"
    },
    {
      "id": "cover_url",
      "type": "image_picker",
      "label": "Thumbnail image",
      "default": ""
    }
  ]
}
</settings>
<!-- #endregion -->

<script>
import btn from "./../components/common/button.vue";
import SvgWrapper from "./../components/common/svg-wrapper.vue";

export default {
  components: {
    "sm-button": btn,
    "svg-wrapper": SvgWrapper,
  },
  props: ["settings", "global_config"],
  watch: {
    settings: function (newVal, oldVal) {
      if (JSON.stringify(newVal) !== JSON.stringify(oldVal)) {
        this.render = false;
        this.showOverlay = !newVal?.props?.autoplay?.value;
        if (this.isYoutube(newVal.props.video_url.value)) {
          this.removeYTScript();
        }
        this.$nextTick(() => {
          this.render = true;
          if (this.isYoutube(newVal.props.video_url.value)) {
            this.loadYTScript();
          }
        });
      }
    },
  },
  computed: {

  },
  beforeMount() {
    this.showOverlay =
      !this.getValueById("autoplay");
  },
  mounted() {
    if (this.isYoutube()) {
      this.loadYTScript();
    }
  },
  data: function () {
    return {
      render: true,
      showOverlay: true,
    };
  },
  methods: {
    loadYTScript() {
      var self = this;
      let nodes = document.querySelectorAll("[data-ytscript]");
      if (nodes.length === 0) {
        var tag = document.createElement("script");
        tag.src = "https://www.youtube.com/iframe_api";
        tag.dataset.ytscript = "true";
        var firstScriptTag = document.getElementsByTagName("script")[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
        tag.onload = () => {
          if (!window.onYouTubeIframeAPIReady) {
            window.onYouTubeIframeAPIReady = function () {
              setTimeout(self.onYouTubeIframeAPIReady.bind(self), 500);
            };
          } else {
            setTimeout(self.onYouTubeIframeAPIReady.bind(self), 500);
          }
        };
      } else {
        if (window.onYouTubeIframeAPIReady) {
          setTimeout(self.onYouTubeIframeAPIReady.bind(self), 500);
        }
      }
    },
    removeYTScript() {
      var players = window.players;
      if (players) {
        Object.keys(players).forEach((item) => {
          players[item].inst && players[item].inst.destroy();
        });
        window.players = null;
      }
      let nodes = document.querySelectorAll("[data-ytscript]");

      if (nodes.length > 0) {
        nodes.forEach((element) => {
          element.parentNode.removeChild(element);
        });
      }
      if (typeof YT !== "undefined") {
        window.YT = undefined;
      }
    },
    isMp4(url = this.getValueById("video_url")) {
      if (!url) {
        return false;
      }
      let ext = url.split(".").pop() || "";
      if (ext && ext.toLowerCase() === "mp4") {
        return true;
      } else {
        return false;
      }
    },
    isYoutube(url = this.getValueById("video_url")) {
      if (!url) {
        return false;
      }
      let urlObj = new URL(url);
      if (
        urlObj.host.includes("youtu.be") ||
        urlObj.host.includes("youtube.com")
      ) {
        return true;
      }
      return false;
    },
    getYTVideoID(url) {
      let urlObj = new URL(url);
      let searchParams = urlObj.searchParams;
      let v = searchParams.get("v");
      if (urlObj.host.includes("youtu.be")) {
        v = urlObj.pathname.split("/").pop();
      }
      return v;
    },
    onYouTubeIframeAPIReady() {
      let ytVideos = document.querySelectorAll(".yt-video");
      // if (!window.players) {
      window.players = {};
      // }
      let players = window.players;
      for (let i = 0; i < ytVideos.length; i++) {
        let node = ytVideos[i];
        let videoID = node.dataset.videoid;
        if (players[videoID]) {
          continue;
        }

        players[videoID] = {};

        let videoMeta = JSON.parse(node.dataset.videometa);
        let qautoplay = videoMeta.autoplay.value,qcontrols = videoMeta.controls.value ? 1 : 0;
        //qmute = videoMeta.autoplay.value;

        players[videoID].onReady = function (e) {
          //if (qmute) {
            //e.target.mute();
          //}
          if (qautoplay) {
            e.target.playVideo();
          }
        };
        players[videoID].onStateChange = function (event) {
          var p = window.players;
          if (event.data == YT.PlayerState.PLAYING) {
            document.getElementById("video_overlay").style.display = "none";
          }

          if (event.data == YT.PlayerState.PAUSED) {
            document.getElementById("video_overlay").style.display = "flex";
          }

          if (event.data == YT.PlayerState.ENDED) {
            p[videoID].inst.seekTo(0);
            p[videoID].inst.playVideo();
          }
        };
        players[videoID].inst = new YT.Player("yt-video-" + videoID, {
          videoId: videoID, // The video id.
          width: "100%",
          height: "100%",
          playerVars: {
            autoplay: qautoplay,
            controls: qcontrols,
            modestbranding: 1,
            mute: qmute,
            loop: 1,
            fs: 0,
            cc_load_policty: 0,
            iv_load_policy: 3,
            origin: document.location.origin,
          },
          events: {
            onReady: players[videoID].onReady,
            onStateChange: players[videoID].onStateChange,
          },
        });
      }
    },
    playMp4() {
      this.showOverlay = false;
      this.$refs.mp4video.play();
    },
    playYT() {
      this.showOverlay = false;
      this.$refs.video_overlay.style.display = "none";
      let videoID = this.$refs.ytVideo.dataset.videoid;
      var p = window.players;
      p[videoID].inst.playVideo();
    },
    playVideo() {
      if (this.isMp4()) {
        this.playMp4();
      } else {
        this.playYT();
      }
    },
  
    checkVideoAutoplay() {
      // returns true if either Autoplay or Video in Background is selected
      return this.getValueById("autoplay");
    },
    checkVideoMute() {
      // returns true if either Autoplay or Video in Background is selected
      return this.checkVideoAutoplay();
    },
    checkVideoControls() {
      //returns false if video controls are disabled or Video in Background is selected
      if (this.getValueById("controls"))
        return true;

      return false;
    },
    getValueById(id) {
      return this.settings?.props?.[id]?.value || "";
    },
  },
};
</script>

<style scoped lang="less">
.video-container {
  position: relative;
  height: 100vh;

  video {
    height: 100%;
    object-fit: cover;
  }

  .yt-container {
    height: 100%;
  }
}

.center-overlay {
  text-align: center;
  inset: 50% auto auto 50%;
  transform: translate(-50%, -50%);
}

.overlay {

  &__image,
  &__color {
    position: absolute;
    inset: 0;
  }

  &__content {
    //min-height: 120px;
    padding: 32px 20px;
    position: absolute;
    width: 637px; //fynd

    @media screen and (max-width: 480px) {
      width: 100%;
    }



    &--text {
      z-index: 2;
      isolation: isolate;
    }

    &.top-left {
      top: 15%;
      left: @header-padding-desktop;

      @media @tablet {
        .center-overlay();
      }
    }

    &.top-center {
      top: 15%;
      left: 50%;
      transform: translateX(-50%);
      text-align: center;

      @media @tablet {
        .center-overlay();
      }
    }

    &.top-right {
      top: 15%;
      right: @header-padding-desktop;
      text-align: right;

      @media @tablet {
        .center-overlay();
      }
    }

    &.center-left {
      left: @header-padding-desktop;
      top: 50%;
      transform: translateY(-50%);

      @media @tablet {
        .center-overlay();
      }
    }

    &.center-center {
      text-align: center;
      .center-overlay(); //idk

      @media screen and (max-width: 768px) {
        bottom: 10%;
        left: 50%;
        transform: translateX(-50%);
        text-align: center;
      }
    }

    &.center-right {
      right: @header-padding-desktop;
      top: 50%;
      transform: translateY(-50%);
      text-align: right;

      @media @tablet {
        .center-overlay();
      }
    }

    &.bottom-left {
      bottom: 10%;
      left: @header-padding-desktop;

      @media @tablet {
        .center-overlay();
      }
    }

    &.bottom-right {
      bottom: 10%;
      right: @header-padding-desktop;
      text-align: right;

      @media @tablet {
        .center-overlay();
      }
    }

    &.bottom-center {
      bottom: 10%;
      left: 50%;
      transform: translateX(-50%);
      text-align: center;

      @media @tablet {
        .center-overlay();
      }
    }
  }

  &__text {
    margin-bottom: 16px;

    h2 {
      font-size: 30px;
      line-height: 31px;
      font-weight: 400;

      @media @mobile {
        font-size: 16px;
      }

      margin-bottom: 16px;
    }

    p {
      font-size: 16px;
      line-height: 24px;

      @media @mobile {
        font-size: 12px;
      }
    }
  }

  .play-button {
    ::v-deep svg {
      width: 80px;
      height: 80px;
      cursor: pointer;
      fill: white;
      opacity: 0.6;
    }

    margin-bottom: 48px;

    @media @tablet {
      margin-bottom: 35px;
    }

    @media @mobile {
      margin-bottom: 30px;
    }
  }
}
</style>
