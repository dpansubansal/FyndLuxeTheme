<template>
    <div>
      <template v-if="settings.props.styleV.value === 'style1'">
        <section :class='["media-with-text" ,"full-width-section"]' >
        <div :class='["media-with-text__content"] '>
          <div class="media-with-text__content--main">
            {{ settings.props.text.value }}
          </div>
        </div>
        <br/>
        <br/>
        <br/>
        <div class="media-with-text__mainBlock">
            <div class="media-with-text__mainBlock--firstBlock">
                <img :src='this.items[0].feature_image.secure_url'/>
                <div class="media-with-text__mainBlock--firstBlock--text">{{this.items[0].title}}</div>
            </div>
            <div class="media-with-text__mainBlock--secondBlock">
                <img :src='this.items[1].feature_image.secure_url' />
                <div class="media-with-text__mainBlock--firstBlock--text">{{this.items[1].title}}</div>
            </div>
            <div class="media-with-text__mainBlock--thirdBlock">
                <img :src='this.items[2].feature_image.secure_url' />
                <div class="media-with-text__mainBlock--firstBlock--text">{{this.items[2].title}}</div>
            </div>
        </div>
        <br/>
        <br/>
        <div class="media-with-text__btn">   
            <sm-button
                :backgroundcolortype="'primary'"
                :colortype="'primary'"
                :bordertype="'primary'"
                :padding="'primary'"
                :global_config="global_config"
                v-if="settings.props.button_text.value"
              >
                {{ settings.props.button_text.value }}
              </sm-button>
          </div>
        </section>
        <div class="whites100"></div>
      </template> 
    
      <template v-if="settings.props.styleV.value === 'style2'">
        <section :class='["media-with-text2" ,"full-width-section"]'>
          <div :class='["media-with-text2__content"] '>
            <div class="media-with-text2__content--main">
              {{ settings.props.text.value }}
            </div>
          </div>
          <br/>
          <br/>
          <br/>
          <div class="media-with-text2__mainBlock">
            <div class="media-with-text2__mainBlock--firstBlock">
              <img :src='this.items[0].feature_image.secure_url' />
              <div class="media-with-text2__mainBlock--firstBlock--text">{{this.items[0].title}}</div>
            </div>
            <div class="media-with-text2__mainBlock--secondBlock">
              <img :src='this.items[1].feature_image.secure_url' />
              <div class="media-with-text2__mainBlock--secondBlock--text">{{this.items[1].title}}</div>
            </div>
          </div>
          <br/>
          <br/>
          <br/>
          <div class="media-with-text2__secondBlock">
              <div class="media-with-text2__secondBlock--firstBlock">
                <img :src='this.items[2].feature_image.secure_url' />
                <div class="media-with-text2__secondBlock--firstBlock--text">{{this.items[2].title}}</div>
              </div>
              <div class="media-with-text2__secondBlock--secondBlock">
                <img :src='this.items[3].feature_image.secure_url' />
                <div class="media-with-text2__secondBlock--secondBlock--text">{{this.items[3].title}}</div>
              </div>
              <div class="media-with-text2__secondBlock--thirdBlock">
                <img :src='this.items[4].feature_image.secure_url' />
                <div class="media-with-text2__secondBlock--thirdBlock--text">{{this.items[4].title}}</div>
              </div>
          </div>
          <br/>
          <br/>
          <div class="media-with-text__btn">   
            <sm-button
                :backgroundcolortype="'primary'"
                :colortype="'primary'"
                :bordertype="'primary'"
                :padding="'primary'"
                :global_config="global_config"
                v-if="settings.props.button_text.value"
              >
                {{ settings.props.button_text.value }}
              </sm-button>
          </div>
        </section>
        <div class="whites100"></div>
      </template>
    
      <template v-if="settings.props.styleV.value === 'style3'">
        <section :class='["media-with-text3" ,"full-width-section"]'>
          <div :class='["media-with-text3__content"] '>
            <div class="media-with-text3__content--main">
              {{ settings.props.text.value }}
            </div>
          </div>
          <br/>
          <br/>
          <br/>
          <div class="media-with-text3__mainBlock">
            <div class="media-with-text3__mainBlock--firstBlock">
              <img :src='this.items[0].feature_image.secure_url' />
              <div class="media-with-text3__mainBlock--firstBlock--text">{{this.items[0].title}}</div>
            </div>
          </div>
          <br/>
          <br/>
          <br/>
          <div class="media-with-text3__secondBlock">
            <div class="media-with-text3__secondBlock--firstBlock">
              <img :src='this.items[1].feature_image.secure_url' />
              <div class="media-with-text3__secondBlock--firstBlock--text">{{this.items[1].title}}</div>
            </div>
            <div class="media-with-text3__secondBlock--secondBlock">
              <img :src='this.items[2].feature_image.secure_url' />
              <div class="media-with-text3__secondBlock--secondBlock--text">{{this.items[2].title}}</div>
            </div>
          </div>
          <br/>
          <br/>
          <div class="media-with-text__btn">   
            <sm-button
                :backgroundcolortype="'primary'"
                :colortype="'primary'"
                :bordertype="'primary'"
                :padding="'primary'"
                :global_config="global_config"
                v-if="settings.props.button_text.value"
              >
                {{ settings.props.button_text.value }}
              </sm-button>
          </div>
        </section>
        <div class="whites100"></div>
      </template>
    </div>
    </template>
    
    <!-- #region  -->
    
    <settings>
    {
      "name": "blog",
      "label": "Blog",
      "props": [
        {
          "type": "select",
          "id": "styleV",
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
          "label": "Layout"
        },
        {
          "type": "text",
          "id": "text",
          "default": "",
          "label": "Heading"
        },
        {
          "type": "text",
          "id": "button_text",
          "default": "View all",
          "label": "Button Text"
        }
      ]
    }
    </settings>
    
    <!-- #endregion -->
    <style lang="less" scoped>
    .media-with-text {
    //   display: flex;
      align-items: center;
      justify-content: space-around;
      font-size: 16px;
      font-weight: 300;
      padding-left: 140px;
      padding-right: 40px;
      box-sizing: border-box;
      @media @large-1280 {
        padding-left: 0px;
        padding-right: 0px;
        flex-direction: column;   
      }
      @media @tablet {
        padding-left: 45px;
      }
      @media @mobile {
        padding-left: 0px;
        text-align-last: center;
      }
      &__btn {
        margin-top: 30px;
        text-align-last: center;
      }
      &__mainBlock {
        display: flex;
        &--firstBlock {
            img {
                width: 394px;
                height: 256px;
            }
            &--text {
              padding-top: 15px;
              text-decoration-line: underline;
            }
            @media screen and (max-width: 768px) {
                img {
                    width: 212px;
                    height: 144px;
                }
                &--text {
                    padding-top: 15px;
                    text-decoration-line: underline;
                }
            }
            @media screen and (max-width: 480px) {
                img {
                    width: 288px;
                    height: 192px;
                }
                &--text {
                    padding-top: 15px;
                    text-decoration-line: underline;
                }
            }
        }
        &--secondBlock {
            padding-left: 25px;
            img {
                width: 394px;
                height: 256px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
            @media screen and (max-width: 768px) {
                img {
                    width: 212px;
                    height: 144px;
                }
                &--text {
                    padding-top: 15px;
                    text-decoration-line: underline;
                }
            }
            @media screen and (max-width: 480px) {
                padding-left: 0px;
                padding-top: 25px;
                img {
                    width: 288px;
                    height: 192px;
                }
                &--text {
                    padding-top: 15px;
                    text-decoration-line: underline;
                }
            }
        }
        &--thirdBlock {
           padding-left: 25px;
           img {
                width: 394px;
                height: 256px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
            @media screen and (max-width: 768px) {
                img {
                    width: 212px;
                    height: 144px;
                }
                &--text {
                    padding-top: 15px;
                    text-decoration-line: underline;
                }
            }
            @media screen and (max-width: 480px) {
                padding-left: 0px;
                padding-top: 25px;
                img {
                    width: 288px;
                    height: 192px;
                }
                &--text {
                    padding-top: 15px;
                    text-decoration-line: underline;
                }
            }
        }
        @media screen and (max-width: 480px) {
            display: flex;
            flex-direction: column;
        }
      }
      &__content {
        // align-self: flex-start;
        text-align-last: center;
        padding-left: 50px;
        padding-right: 50px;
        display: flex;
        flex-direction: column;
        line-height: 35px;
        box-sizing: border-box;
        
        &--main {
          padding: 10px;
          font-size: 32px;
          font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
          font-weight: 300;
          line-height: 36px;
        }
      }
    }
    .media-with-text2 {
      align-items: center;
      justify-content: space-around;
      font-size: 16px;
      font-weight: 300;
      padding-left: 105px;
      padding-right: 40px;
      box-sizing: border-box;
      @media @large-1280 {
        padding-left: 0px;
        padding-right: 0px;
        flex-direction: column;
      }
      @media @tablet {
        padding-left: 45px;
      }
      @media @mobile {
        padding-left: 0px;
        text-align-last: center;
      }
      &__btn {
        margin-top: 30px;
        text-align-last: center;
      }
      &__content {
        // align-self: flex-start;
        text-align-last: center;
        padding-left: 50px;
        padding-right: 50px;
        display: flex;
        flex-direction: column;
        line-height: 35px;
        box-sizing: border-box;
        
        &--main {
          padding: 10px;
          font-size: 32px;
          font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
          font-weight: 300;
          line-height: 36px;
        }
      }
      &__mainBlock {
        display: flex;
        &--firstBlock {
          img {
            width: 628px;
            height: 336px;
          }
          &--text {
            padding-top: 15px;
            text-decoration-line: underline;
          }
          @media screen and (max-width: 768px) {
            img {
              width: 325px;
              height: 208px;
            }
            &--text {
              padding-top: 15px;
              text-decoration-line: underline;
            }
          }
          @media screen and (max-width: 480px) {
            img {
              width: 301px;
              height: 192px;
            }
            &--text {
              padding-top: 15px;
              text-decoration-line: underline;
            }
          }
        }
        &--secondBlock {
          padding-left: 40px;
          img {
            width: 628px;
            height: 336px;
          }
          &--text {
            padding-top: 15px;
            text-decoration-line: underline;
          }
          @media screen and (max-width: 768px) {
            padding-left: 14px;
            img {
              width: 325px;
              height: 208px;
            }
            &--text {
              padding-top: 15px;
              text-decoration-line: underline;
            }
          }
          @media screen and (max-width: 480px) {
            padding-left: 0px;
            padding-top: 25px;
            img {
              width: 301px;
              height: 192px;
            }
            &--text {
              padding-top: 15px;
              text-decoration-line: underline;
            }
          }
        }
        @media screen and (max-width: 480px) {
            display: flex;
            flex-direction: column;
        }
      }
      &__secondBlock::-webkit-scrollbar {
        display: none;
      }
      &__secondBlock {
        display: flex;
        overflow: auto;
        &--firstBlock {
          img {
            width: 405px;
            height: 240px;
          }
          &--text {
            padding-top: 15px;
            text-decoration-line: underline;
          }
          @media screen and (max-width: 768px) {
            img {
                width: 212px;
                height: 144px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
          @media screen and (max-width: 480px) {
            img {
                width: 212px;
                height: 144px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
        }
        &--secondBlock {
          padding-left: 40px;
          img {
            width: 406px;
            height: 240px;
          }
          &--text {
            padding-top: 15px;
            text-decoration-line: underline;
          }
          @media screen and (max-width: 768px) {
            padding-left: 14px;
            img {
                width: 212px;
                height: 144px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
          @media screen and (max-width: 480px) {
            img {
                width: 212px;
                height: 144px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
        }
        &--thirdBlock {
          padding-left: 40px;
          img {
            width: 405px;
            height: 240px;
          }
          &--text {
            padding-top: 15px;
            text-decoration-line: underline;
          }
          @media screen and (max-width: 768px) {
            padding-left: 14px;
            img {
              width: 212px;
              height: 144px;
            }
            &--text {
              padding-top: 15px;
              text-decoration-line: underline;
            }
          }
          @media screen and (max-width: 480px) {
            padding-left: 14px;
            padding-right: 14px;
            img {
                width: 212px;
                height: 144px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
        }
        @media screen and (max-width: 480px) {
          padding-left: 35px;
        }
      }
    }
    .media-with-text3 {
      align-items: center;
      justify-content: space-around;
      font-size: 16px;
      font-weight: 300;
      padding-left: 115px;
      padding-right: 40px;
      box-sizing: border-box;
      @media @large-1280 {
        padding-left: 0px;
        padding-right: 0px;
        flex-direction: column;
      }
      @media @tablet {
        padding-left: 55px;
      }
      @media @mobile {
        padding-left: 0px;
        text-align-last: center;
      }
      &__btn {
        margin-top: 30px;
        text-align-last: center;
      }
      &__content {
        // align-self: flex-start;
        text-align-last: center;
        padding-left: 50px;
        padding-right: 50px;
        display: flex;
        flex-direction: column;
        line-height: 35px;
        box-sizing: border-box;
        
        &--main {
          padding: 10px;
          font-size: 32px;
          font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
          font-weight: 300;
          line-height: 36px;
        }
      }
      &__mainBlock {
        &--firstBlock {
          img {
            width: 1296px;
            height: 512px;
          }
          &--text {
            padding-top: 15px;
            text-decoration-line: underline;
          }
          @media screen and (max-width: 768px) {
            img {
              width: 664px;
              height: 328px;
            }
            &--text {
              padding-top: 15px;
              text-decoration-line: underline;
            }
          }
          @media screen and (max-width: 480px) {
            img {
              width: 301px;
              height: 192px;
            }
            &--text {
              padding-top: 15px;
              text-decoration-line: underline;
            }
          }
        }
        @media screen and (max-width: 480px) {
            display: flex;
            flex-direction: column;
        }
      }
      &__secondBlock::-webkit-scrollbar {
        display: none;
      }
      &__secondBlock {
        display: flex;
        overflow: auto;
        &--firstBlock {
          img {
            width: 628px;
            height: 336px;
          }
          &--text {
            padding-top: 15px;
            text-decoration-line: underline;
          }
          @media screen and (max-width: 768px) {
            img {
                width: 325px;
                height: 192px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
          @media screen and (max-width: 480px) {
            img {
                width: 212px;
                height: 144px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
        }
        &--secondBlock {
          padding-left: 40px;
          img {
            width: 628px;
            height: 336px;
          }
          &--text {
            padding-top: 15px;
            text-decoration-line: underline;
          }
          @media screen and (max-width: 768px) {
            padding-left: 14px;
            img {
                width: 325px;
                height: 192px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
          @media screen and (max-width: 480px) {
            padding-left: 14px;
            padding-right: 14px;
            img {
                width: 212px;
                height: 144px;
            }
            &--text {
                padding-top: 15px;
                text-decoration-line: underline;
            }
          }
        }
        @media screen and (max-width: 480px) {
          padding-left: 35px;
        }
      }
    }
    .media-with-text3 ,.media-with-text2 ,.media-with-text {
      position: relative;
    }
    .whites100{
      position: absolute;
      top:0px;
      left:0px;
      width: 100%;
      height: 100%;
      background-color: white;
      animation-name: example100;
      animation-duration: 1.5s;
      animation-direction:reverse;
      animation-fill-mode: forwards;
    }
    @keyframes example100 {
      0%   {height:0%;}
      100% {height:100%;}
    }
    </style>
    
    <script>
    import NoSSR from "vue-no-ssr";
    import "video.js/dist/video-js.min.css";
    import btn from "./../components/common/button.vue";
    export default {
      data() {
        return {
         items: []
        };
      },
      props: ["settings", "context", "global_config"],
      computed: {
       
      },
      methods: {
        fetchData() {
            console.log("Inside func");
          this.$apiSDK.content.getBlogs({pageNo : 1 ,pageSize : 5}).then((data) => {
            console.log("Data from Blog API", data);
            this.items = data.items;
            console.log("Items Title", this.items[0].title);
            console.log("Items Image", this.items[0].feature_image.secure_url);
          });
        }
      },
      components: {
        "sm-button": btn,
        "no-ssr": NoSSR
      },
      mounted() {
        this.fetchData();
        console.log("Setting Data from Blog", this.settings);
      }
    };
    </script>