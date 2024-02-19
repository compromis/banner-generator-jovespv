<template>
  <div
    :id="'bannerCanvas' + aspect"
    :class="[
      'banner-canvas',
      'aspect-' + aspect,
      aspect === '11' ? 'disposition-' + banner.disposition : '',
      banner.localLabel && banner.hasLocalLabel ? 'has-local-label' : '',
      'blobs-' + color
    ]"
    v-if=true>
    <div :id="'image' + color" class="blob blob-image">
      <img class="picture" :src="banner.picturePreview" alt="Imatge" v-if="banner.picturePreview" :style="objectPosition" />
      <div class="quatribarrada" v-if="this.color == 'red'">
        </div>
    </div>
    <div class="Avant">
      <Avant class="Avant" :mono="true"></Avant>
    </div>
    <div class="text text-wysiwyg" v-if="banner.text">
      <div v-html="banner.text"></div>
    </div>
    <emojis-on-canvas v-model="banner.emojis" />
    <div class="logo">
      <compromis-logo :mono="true" v-if="!banner.name"/>
    </div>
    <div class="logo" v-if="banner.name && aspect == '11'" style="bottom: 15px; right: 17px;" >
      <TextColectiu class="nomcolectiu" :mono="true" :logoStyle="banner.name" style="height: 80px;"></TextColectiu>
    </div>
    <div class="logo" v-if="banner.name && aspect == '916'" style="bottom: 55px; left: 55px; width: 300px;" >
      <TextColectiu class="nomcolectiu" :mono="true" :logoStyle="banner.name" style="height: 80px;"></TextColectiu>
    </div>
    <div class="hashtag" v-if="aspect">
      {{ banner.hashtag }}
    </div>
  </div>
</template>

<script>
import CanvasMixin from '@/mixins/canvas-mixin.js'
import EmojisOnCanvas from '@/utils/EmojisOnCanvas'
import TextColectiu from '@/utils/ColectiuLogo'
import Avant from '@/utils/Avant'

export default {
  name: 'text-canvas',

  mixins: [CanvasMixin],

  components: {
    EmojisOnCanvas,
    TextColectiu,
    Avant
  }
}
</script>

<style lang="scss" scoped>
  @import "../../../sass/variables";

 
.text {
  position: absolute;
    color: $white;
    bottom: 43%; /* Lo posiciona un poco más abajo del centro */
    left: 50%;
    transform: translate(-50%, 50%); /* Lo centra horizontalmente y un poco más abajo */
    z-index: 30;
    padding: 0px 0px;
    max-height: 700px;
    overflow: hidden;
    font-family: 'Avant';
    font-size: 50px; /* Ajusta el tamaño de la fuente según tus necesidades */
    white-space: nowrap;
    text-align: right; /* Justifica el texto a la derecha */
}



  .Avant {
    z-index: 30;
    top: 110px;
    left: 17px;
    width: 95%;
    position: absolute;
    stroke-width: 5px;
  }
  .blob {
    &-1 {
      left: -58%;
      top: -82%;
      z-index: 20;
    }

    &-2 {
      right: -57%;
      bottom: -81%;
      z-index: 20;
      --gradient-orientation: -45deg;
    }

    &-image {
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      height: 100%;
      width: 100%;
      z-index: 10;
      background: $gray-300;
      transform: rotate(0);
      border-radius: 0;

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transform: rotate(0);
      }
    }
  }

  .logo {
    color: $white;
    z-index: 10;
    position: absolute;
    bottom: 20px; /* Distancia desde la parte inferior */
    left: 50%; /* Posición en el centro horizontal */
    transform: translateX(-45%); /* Centra el elemento horizontalmente */
    margin-bottom: 20px; /* Margen adicional desde la parte inferior */
}

.logo-local-label {
    color: $white;
}


  .hashtag {
    color: $white;
    top: 587px;
    left: 304px;
    width: 245px;
    text-align: center;
  }

  .has-local-label {
    .blob-2 {
      right: -40%;
    }
  }

  #imagenormal {
    background: radial-gradient(circle at center, rgba(255, 127, 0, 1) 30%, rgba(255, 106, 0, 0.8) 40%, rgba(255, 87, 0, 0.6) 70%, rgba(255, 47, 0, 0.4) 90%, rgba(255, 0, 0, 0.2) 120%);
    height: 820px;
}

.picture {
    width: 100%;
    height: 100%;
    object-fit: cover;
    mix-blend-mode: multiply;
}


  #imagefeminista{
    background: radial-gradient(circle at top left, rgba(109,35,127,1) 0%, rgba(109,35,127,0.60) 50%, rgba(109,35,127,0) 100%);
    height: 720px;

    .picture {
      width: 100%;
      height: 100%;
      object-fit: cover;
      mix-blend-mode: multiply;
    }
  }

  #imagegreen{
    background: radial-gradient(circle at top left, rgba(9,128,55,1) 0%, rgba(9,128,55,0.60) 50%, rgba(19,128,55,0) 100%);
    height: 720px;

    .picture {
      width: 100%;
      height: 100%;
      object-fit: cover;
      mix-blend-mode: multiply;
    }
  }

  #imagered{
    background: radial-gradient(circle at top left, rgba(224,14,24,1) 100%, rgba(224,14,24,0.60) 50%, rgba(233, 66, 10, 0) 100%);
    height: 720px;

    .picture {
      width: 100%;
      height: 100%;
      object-fit: cover;
      mix-blend-mode: multiply;
    }
  }

  #imagelgtb{
    background: linear-gradient(135deg, rgba(109,35,127,1) 0%, rgba(48,87,161,1) 21%, rgba(9,128,55,1) 41%, rgba(248,231,32,1) 62%, rgba(239,134,26,1) 82%, rgba(224,14,24,1) 100%);
    height: 720px;

    .picture {
      width: 100%;
      height: 100%;
      object-fit: cover;
      mix-blend-mode: multiply;
    }
  }

  // Story aspect
  .aspect-916 {

    .text {
      left: 50px;
      right: 50px;
      top: 115px;
      bottom: 300px;
      padding: 16px;
    }

    .logo {
      width:250px;
      left: 80px;
      bottom: 80px;
    }

    .marc {
      z-index: 30;
      top: 105px;
      left: 40.5px;
      width: 80%;
      position: absolute;
    }

    .hashtag {
    color: $white;
    top: 412px;
    left: 160px;
    width: 167px;
    text-align: center;
  }
  }

</style>

<style lang="scss">
  @import "../../../sass/variables";

  .text-wysiwyg {
    font-size: 20px;

    & > div > *:first-child {
      margin-top: 0;
    }

    & > div > *:last-child {
      margin-bottom: 0;
    }

    & > div > h2:first-child {
      margin-top: -24px;
    }

    & > div > h2:last-child {
      margin-bottom: -24px;
    }

    h1 {
      font-size: 40px;
      letter-spacing: -1px;
      font-weight: bold;
      margin: 16px 0;
      line-height: 1.1;
    }

    h2 {
      padding: 16px 24px;
      margin: 16px -24px;
      font-size: 24px;
      font-weight: bold;
      letter-spacing: -.5px;
      line-height: 1.1;
    }

    p {
      line-height: 1.1;
      margin: 16px 0;
    }

    ol {
      margin: 16px 0;

      li {
        margin-left: 30px;
        line-height: 1;
        margin-bottom: 12px;
      }
    }

    ul {
      margin: 16px 0;

      li {
        padding-left: 30px;
        line-height: 1;
        margin-bottom: 12px;

        &::before {
          position: absolute;
          content: '➡️';
          color: $white;
          font-weight: bold;
          left: 24px;
        }
      }

      &[data-checked] {
        li::before {
          content: '✅';
        }
      }
    }

    u {
      color: $orange;
    }
  }

  .aspect-916 {
    .text-wysiwyg {
      & > div > h2:first-child {
        margin-top: -16px;
      }

      & > div > h2:last-child {
        margin-bottom: -16px;
      }

      h2 {
        padding: 16px;
        margin: 16px -16px;
        font-size: 20px;
      }

      ul {
        li {
          padding-left: 28px;

          &::before {
            left: 16px;
          }
        }
      }
    }
  }
</style>
