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
    <emojis-on-canvas v-model="banner.emojis" />
    <div class="logo">
      <compromis-logo :mono="true" v-if="!banner.name"/>
    </div>
    <div class="logo11" v-if="banner.name && aspect == '11'" style="bottom: 15px; right: 17px;" >
      <TextColectiu class="nomcolectiu" :mono="true" :logoStyle="banner.name" style="height: 80px;"></TextColectiu>
    </div>
    <div class="logo916" v-if="banner.name && aspect == '916'">
      <TextColectiu class="nomcolectiu" :mono="true" :logoStyle="banner.name" style="height: 80px;"></TextColectiu>
    </div>
    <div class="Edicio" v-if="banner.Edicio">
      <div v-html="banner.Edicio"></div>
    </div>
    <div class="text" v-if="banner.text">
      <div v-html="banner.text"></div>
    </div>
    <div class="Lloc" v-if="banner.Lloc">
      <div v-html="banner.Lloc"></div>
    </div>
    <div class="Calendar" contenteditable>
          <b-icon icon="calendar-day"/> {{ banner.date | formatDate }}
        </div>
        <div class="Clock" contenteditable>
          <b-icon icon="clock"/> {{ banner.time | formatTime }}
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
  bottom: 38%; 
  z-index: 10;
  font-family: 'Avant';
  font-size: 50px; 
  white-space: nowrap;
  text-align: right; 
  right: 0; 
  padding-right: 50px;
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
  .Calendar {
  color: rgb(255, 255, 255);
  top: 73%;
  left: 50%;
  transform: translateX(-45%);
  width: 220px; /* Ajusta el ancho según tus necesidades */
  position: absolute;
  z-index: 10;
  font-size: 16px;
  font-family: 'AvantN';
}

.Clock {
  color: rgb(255, 255, 255);
  top: 77%;
  left: 50%;
  transform: translateX(-45%);
  width: 80px; /* Ajusta el ancho según tus necesidades */
  position: absolute;
  z-index: 10;
  font-size: 16px;
  font-family: 'AvantN';
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

.logo11 {
    color: $white;
    z-index: 10;
    position: absolute;
    bottom: 20px; /* Distancia desde la parte inferior */
    left: 50%; /* Posición en el centro horizontal */
    transform: translateX(-55%); /* Centra el elemento horizontalmente */
    margin-bottom: 20px; /* Margen adicional desde la parte inferior */
}


.logo-local-label {
    color: $white;
}



  .Edicio {
  color: $white;
  position: absolute;
  z-index: 10;
  top: 10%; /* Lo posiciona en el centro vertical */
  left: 50%; /* Lo posiciona en el centro horizontal */
  width: 245px;
  text-align: center; /* Centra el texto horizontalmente */
  transform: translate(-50%, -50%); /* Lo centra exactamente en el medio del contenedor */
  font-family: 'Avant';
  font-size: 20px; /* Ajusta el tamaño de la fuente según tus necesidades */
}
.Lloc {
  color: $white;
  position: absolute;
  z-index: 10;
  top:71%; /* Lo posiciona en el centro vertical */
  left: 50%; /* Lo posiciona en el centro horizontal */
  width: 400px;
  text-align: center; /* Centra el texto horizontalmente */
  transform: translate(-50%, -50%); /* Lo centra exactamente en el medio del contenedor */
  font-family: 'AvantN';
  font-size: 16px; /* Ajusta el tamaño de la fuente según tus necesidades */
}

  .has-local-label {
    .blob-2 {
      right: -40%;
    }
  }

  #imagenormal {
    background: radial-gradient(circle at center, rgba(255, 127, 0, 1) 30%, rgba(255, 106, 0, 0.8) 40%, rgba(255, 85, 0, 0.841) 70%, rgba(255, 47, 0, 0.732) 90%, rgba(255, 0, 0, 0.2) 120%);
    height: 820px;
}

.picture {
    width: 100%;
    height: 100%;
    object-fit: cover;
    mix-blend-mode: multiply;
}


  #imagefeminista{
    background: radial-gradient(circle at top center , rgb(201, 99, 226) 30%, rgba(161, 44, 190, 0.945) 50%, rgba(79, 1, 99, 0.967) 100%);
    height: 720px;

    .picture {
      width: 100%;
      height: 100%;
      object-fit: cover;
      mix-blend-mode: multiply;
    }
  }

  #imagegreen{
    background: radial-gradient(circle at top center, rgb(65, 196, 115) 50%, rgb(9, 132, 56) 70%, rgb(8, 77, 31) 100%);
    height: 720px;

    .picture {
      width: 100%;
      height: 100%;
      object-fit: cover;
      mix-blend-mode: multiply;
    }
  }

  #imagered{
    background: radial-gradient(circle at top center, rgba(224,14,24,1) 40%, rgb(224, 14, 24) 50%, rgb(0, 0, 0) 100%);
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
  position: absolute;
  color: $white;
  bottom: 47%; 
  z-index: 10;
  font-family: 'Avant';
  font-size: 25px; 
  white-space: nowrap;
  text-align: right; 
  right: 0; 
  padding-right: 30px;
}


  .Avant {
    z-index: 30;
    top: 130px;
    left: 10px;
    width: 95%;
    position: absolute;
    stroke-width: 5px;
  }

    .logo {
      width:250px;
      left: 190px;
      bottom: 50px;
    }
   
    .logo916 {
  color: white;
  position: absolute;
  z-index: 20;
  width: 250px;
  left: 38%; /* Centra horizontalmente */
  transform: translateX(-50%) scale(0.7); /* Centra exactamente en el medio y reduce el tamaño */
  bottom: 20px;
}

.Calendar {
  color: rgb(255, 255, 255);
  top: 73%;
  left: 52%;
  transform: translateX(-45%);
  width: 220px; /* Ajusta el ancho según tus necesidades */
  position: absolute;
  z-index: 10;
  font-size: 15px;
  font-family: 'AvantN';
}

.Clock {
  color: rgb(255, 255, 255);
  top: 77%;
  left: 48%;
  transform: translateX(-45%);
  width: 80px; /* Ajusta el ancho según tus necesidades */
  position: absolute;
  z-index: 10;
  font-size: 15px;
  font-family: 'AvantN';
}
.Lloc {
  color: $white;
  position: absolute;
  z-index: 10;
  top:71%; /* Lo posiciona en el centro vertical */
  left: 50%; /* Lo posiciona en el centro horizontal */
  width: 400px;
  text-align: center; /* Centra el texto horizontalmente */
  transform: translate(-50%, -50%); /* Lo centra exactamente en el medio del contenedor */
  font-family: 'AvantN';
  font-size: 15px; /* Ajusta el tamaño de la fuente según tus necesidades */
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
