<template>
  <div
    :id="'bannerCanvas' + aspect"
    :class="[
      'banner-canvas',
      'aspect-' + aspect,
      aspect === '11' || banner.card ? 'disposition-' + banner.disposition : '',
      banner.card ? 'cards' : 'no-cards',
      banner.localLabel && banner.hasLocalLabel ? 'has-local-label' : '',
      banner.headline.length > 95 ? 'has-long-headline' : '',
      'blobs-'
    ]"
    v-if="banner">
    <div class="blob blob-image">
      <img :src="banner.picturePreview" alt="Imatge" v-if="banner.picturePreview" :style="objectPosition" />
    </div>
    <div class="blob blob-1"></div>
    <div class="headline">
      <div class="headline-text"
        :style="{
          fontFamily: banner.source ? banner.source.fontFamily : false,
          fontSize: aspect === '11' ? fontSize(banner.headline, 50, 27, 160) : fontSize(banner.headline, 35, 21, 160),
          letterSpacing: banner.source ? banner.source['letterSpacing'] : false
        }">
        {{ banner.headline | formatString }}
      </div>
      <div class="headline-source headline-source--custom" v-if="banner.source === 'other'" :style="banner.card ? { backgroundColor: banner.customSourceColor } : null">
        <span :style="banner.card ? { color: 'white' } : { color: banner.customSourceColor }">{{ banner.customSource }}</span>
      </div>
      <div class="headline-source" v-else-if="banner.source" :style="banner.card ? { backgroundColor: banner.source.color } : null">
        <img :src="banner.source.hasOwnProperty('logoCard') && banner.card ? banner.source.logoCard : banner.source.logo" :alt="banner.source.name" :style="{ height: banner.source.logoHeight + 'px' }" />
      </div>
    </div>
    <emojis-on-canvas v-model="banner.emojis" />

    <div class="marc">
      <Forquilla class="marcgeneric"></Forquilla>
    </div>
    <div>
      <Forquilla class="marcgeneric" v-if="this.color == 'normal'">></Forquilla>
    </div>
    <div class="marc">
      <Forquilla class="marcgeneric" v-if="this.color == 'feminista'" :feminista="true"></Forquilla>
    </div>
    <div class="marc">
      <Forquilla class="marcgeneric" v-if="this.color == 'lgtb'" :lgtb="true">> </Forquilla>
    </div>
    <div class="marc">
      <Forquilla class="marcgeneric" v-if="this.color == 'green'" :green="true">> </Forquilla>
    </div>
    <div class="marc">
      <Forquilla class="marcgeneric" v-if="this.color == 'red'" :red="true">> </Forquilla>
    </div>

    <div class="logo">
      <compromis-logo :mono="true" v-if="!banner.name"/>
    </div>
    <div class="logo" v-if="banner.name && aspect == '11'" style="bottom: 15px; right: 17px;" >
      <TextColectiu class="nomcolectiu" :mono="true" :logoStyle="banner.name" style="height: 80px;"></TextColectiu>
    </div>
    <div class="logo" v-if="banner.name && aspect == '916'" style="bottom: 55px; left: 55px; width: 300px;" >
      <TextColectiu class="nomcolectiu" :mono="true" :logoStyle="banner.name" style="height: 80px;"></TextColectiu>
    </div>
    <div class="hashtag" v-if="!banner.name">
      {{ banner.hashtag }}
    </div>
    <div class="hashtag2" v-if="aspect && banner.name">
      {{ banner.hashtag }}
    </div>
    <div :id="'blob-2' + color" class="blob blob-2"></div>
  </div>
</template>

<script>
import CanvasMixin from '@/mixins/canvas-mixin.js'
import EmojisOnCanvas from '@/utils/EmojisOnCanvas'
import TextColectiu from '@/utils/ColectiuLogo'
import Forquilla from '@/utils/forquilla'

export default {
  name: 'headline-canvas',

  mixins: [CanvasMixin],

  components: {
    EmojisOnCanvas,
    Forquilla,
    TextColectiu
  }
}
</script>

<style lang="scss" scoped>
  @import "../../../sass/variables";
  @import "./fonts";

  .headline {
    display: flex;
    position: absolute;
    left: 70px;
    z-index: 30;

    width: 500px;
    padding: 10px 40px;
    font-family: 'Tiempos Headline', serif;
    font-weight: 700;
    transition: all .5s ease-in-out;
    flex-direction: column;
    align-items: center;

    &-source {

      &--custom {
        margin-bottom: 4px;
        font-size: 22px;
      }
    }

    &-text {
      font-size: 23px;
      line-height: 1.1;
      word-wrap: break-word;
      height: 180px;
      text-align: center;
    }
  }

  .marc {
    z-index: 30;
    position: absolute;
    width: 83%;
    top: -371px;
    left: 72px;
  }
  .blob {

    &-1 {
      background: $white;
      transform: rotate(0);
      width: 85%;
      top: -495px;
      left: 55px;

    }
    &-image {
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        transform: rotate(0);
        border-radius: 0;
        z-index: 0;

        img {
          transform: rotate(0);
          width: 100%;
          margin: 0;
        }
    }
    &-2 {
      z-index: 20;
      bottom: -130px;
      right: -50px;
      width: 600px;
      height: 300px;
      transform: rotate(0);
    }
  }

  #blob-2normal {
    background: radial-gradient(at 500px 150px, rgba(232,93,15,0.6) 0%, rgba(232,93,15,0) 65%);
  }

  #blob-2feminista{
    background: radial-gradient(at 500px 150px, rgba(109,35,127,1) 0%, rgba(109,35,127,0) 65%);
  }

  #blob-2green{
    background: radial-gradient(at 500px 150px, rgba(9,128,55,1) 0%, rgba(19,128,55,0) 65%);
  }

  #blob-2red{
    background: radial-gradient(at 500px 150px, rgba(224,14,24,1) 0%, rgba(19,128,55,0) 65%);
  }

  #blob-2lgtb{
    border-radius: 0;
    bottom: 0;
    right: 0;
    opacity: .6;
    width: 720px;
    height: 85px;
    background: linear-gradient(90deg,
      rgba(239,64,77,1) 0%,
      rgba(239,64,77,1) 16.6%,
      rgba(247,146,38,1) 16.6%,
      rgba(247,146,38,1) 33.2%,
      rgba(255,209,15,1) 33.2%,
      rgba(255,209,15,1) 49.8%,
      rgba(127,195,71,1) 49.8%,
      rgba(127,195,71,1) 66.4%,
      rgba(85,164,219,1) 66.4%,
      rgba(85,164,219,1) 83%,
      rgba(161,74,156,1) 83%,
      rgba(161,74,156,1) 100%);
  }

  .hashtag {
    position: absolute;
    z-index: 30;
    bottom: 25px;
    left: 35px;
    color: $white;
    font-weight: bold;
    font-size: 20px;
    letter-spacing: -0.3px;
  }
  .hashtag2 {
    position: absolute;
    z-index: 30;
    bottom: 25px;
    left: 35px;
    color: $white;
    font-weight: bold;
    font-size: 20px;
    letter-spacing: -0.3px;
    bottom: 40px;
  }

  .logo {
    color: $white;
    z-index: 50;
  }

  .has-local-label {
    .blob-2 {
      left: -60%;
    }
  }

  // Square aspect
  .aspect-11 {
    .blob-image {
      border-bottom-left-radius: 0;
    }
  }

  // Story aspect
  .aspect-916 {
    .headline {
      display: flex;
      position: absolute;
      left: 13px;
      z-index: 30;
      width: 300px;
      margin-top: 80px;
      padding: 10px 40px;
      font-family: 'Tiempos Headline', serif;
      font-weight: 700;
      transition: all .5s ease-in-out;
      flex-direction: column;
      align-items: center;

      &-source {
          position: absolute;
          top: 167px;

        &--custom {
          margin-bottom: 4px;
          font-size: 22px;
        }

        img {
          width: 65px;
          height: 20px;
          object-fit: contain;
        }
      }

      &-text {
        font-size: 23px;
        line-height: 1.1;
        word-wrap: break-word;
        height: auto;
        text-align: center;
        overflow: hidden;

      }
    }
      &-image {
        top: -20px;
        left: -12px;
        width: 444px;
        height: 395px;
        border-bottom-right-radius: 0;

        img {
          width: 93%;
          margin: 15px 10px;
        }
      }

      .marc {
        width: 85%;
        top: -68px;
        left: 38px;
      }

      .blob {

        &-1 {
          background: $white;
          transform: rotate(0);
          width: 90%;
          top: -440px;
          left: 20px;
          border-radius: 3rem;
        }
      }
    }

    .headline {
      //top: 430px;

      &-text {
        font-size: 20px;
      }
    }

  // Headline on top
  .disposition-1.no-cards {
    .headline {
      top: 90px;
      height: 172px;
    }

    .blob-image {
      img {
        margin: -29px -14px;
      }
    }

    .logo {
      bottom: 666px;
    }

    .hashtag {
      bottom: 668px;
    }

    .blob {
      &-1 {
        top: -90%;
        right: 40%;
      }

      &-2 {
        opacity: 0;
      }

      &-image {
        border-top-left-radius: $border-radius;
        border-bottom-left-radius: 0;
        border-bottom-right-radius: 0;
        top: 285px;
        left: 130px;
        height: 500px;
      }
    }
  }

  /* Card style */
  .cards {
    .headline {
      z-index: 30;
      left: 40px;
      right: 40px;
      bottom: 90px;
      top: auto;
      background: $white;
      box-shadow: $raised-shadow;
      border-radius: $card-radius;
      height: auto;
      padding: 26px;
      overflow: hidden;

      &-source {
        background: $green;
        margin: -26px -26px 26px -26px;
        padding: 8px 26px;

        img {
          position: relative;
          top: 3px;
          filter: grayscale(100%) brightness(0) invert(1);
        }

        &--custom {
          font-size: 22px;
          color: $white;
          font-family: Compromis, sans-serif;
        }
      }
    }

    .blob {
      &-1 {
        left: -58%;
        top: -82%;
        z-index: 20;
      }

      &-2 {
        left: auto;
        right: -57%;
        bottom: -81%;
        z-index: 20;
        --gradient-orientation: -45deg;
      }

      &-image {
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        transform: rotate(0);
        border-radius: 0;
        z-index: 0;

        img {
          transform: rotate(0);
          width: 100%;
          margin: 0;
        }
      }
    }

    .logo {
      z-index: 30;
      color: $white;
    }

    .hashtag {
      top: 20px;
      left: 35px;
      bottom: auto;
    }

    /* Cards with headline on top */
    &.disposition-1 {
      .headline {
        top: 88px;
        bottom: auto;
      }
    }

    /* Cards in story aspect */
    &.aspect-916 {
      .headline {
        left: 16px;
        right: 16px;
        padding: 18px;

        &-source {
          margin: -18px -18px 18px -18px;
          padding: 8px 18px;
        }
      }

      .blob {
        &-1 {
          left: -118%;
        }

        &-2 {
          right: -104%;
        }
      }

      /* Cards in story aspect with headline on top */
      &.disposition-1 {
        .headline {
          top: 88px;
          bottom: auto;
        }
      }
    }
  }

  .no-cards .drr {
    display: none;
  }
</style>
