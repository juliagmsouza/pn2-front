<template>
  <div :class="backgroundMapper[albums[index].name.toLowerCase()]" id="app">
    <div>
      <trash-icon
          size="6x"
          style="cursor: pointer"
          >
        </trash-icon>
        <edit-icon
          size="6x"
          style="cursor: pointer"
          >
        </edit-icon>
      oiaaaa
    </div>
    <div class="d-flex h-80 align-items-center"> 
      <b-row class="w-100" align-h="center">
        <b-col class="align-self-center d-flex justify-content-end">
          <chevron-left-icon
          style="cursor: pointer"
          size="6x"
          @click="previousAlbum"
          >
        </chevron-left-icon>
        </b-col>
        <b-col class="d-flex justify-content-center" cols="3">
          <b-img v-if="albums[index - 1]" :src="albums[index - 1].image_url" class="rounded image-size">
          </b-img>
          <b-img v-else :src="albums[albums.length - 1].image_url" class="rounded image-size">
            </b-img>
        </b-col>
        <b-col class="d-flex justify-content-center position-relative" cols="3">
          <b-img :src="albums[index].image_url" class="rounded image-size detail-album-image" @mouseover="hover=true" @mouseleave="hover=false">
          </b-img>
          <div v-if="hover" class="detail-album-content rounded">
            <b-row class="pt-2">
              Álbum: {{ albums[index].name }}, {{ albums[index].year }} - {{ albums[index].recorder }}
            </b-row>
            <b-row class="pt-1 align-text">
              Descrição: {{ albums[index].description }}
            </b-row>
            <b-row class="pt-1">
              Faixas: 
              <ul>
                <li v-for="i, index in albums[index].tracks" :key="index">{{i}}</li>
              </ul>
            </b-row>
            <b-row style="margin-top: -10px">
              Valor: R$ {{ albums[index].valor }}
            </b-row>
          </div>
        </b-col>
        <b-col class="d-flex justify-content-center" cols="3">
          <b-img v-if="albums[index + 1]" :src="albums[index + 1].image_url" class="rounded image-size">
          </b-img>
          <b-img v-else :src="albums[0].image_url" class="rounded image-size"></b-img>
        </b-col>
        <b-col class="align-self-center">
          <chevron-right-icon
          size="6x"
          style="cursor: pointer"
          @click="nextAlbum"
          >
        </chevron-right-icon>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
import { ChevronLeftIcon, ChevronRightIcon, TrashIcon, EditIcon} from 'vue-feather-icons'

export default {
  components: {
    EditIcon,
    TrashIcon,
    ChevronLeftIcon,
    ChevronRightIcon,
  },
  name: 'App',
  data() {
    return {
      hover: false,
      index: 1,
      selectedAlbum: {
        name: 'evermore'
      },
      albums: [
        {
          id: 1,
          name: "evermore",
          valor: "150.75",
          year: "2020",
          image_url: 'https://people.com/thmb/CzW6mR0ScLNkUegGLPM4p6LBSDE=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc():focal(749x0:751x2):format(webp)/taylor-swift-1-1bd711adc60c4534926738641a2acf2f.jpg',
          description: 'Evermore é o nono álbum de estúdio da cantora e compositora estadunidense Taylor Swift. O seu lançamento ocorreu em 11 de dezembro de 2020, através da gravadora Republic Records, menos de cinco meses após Folklore, seu oitavo álbum de estúdio.',
          recorder: 'Republic Records',
          tracks: [
            'willow',
            'champagne problems',
            'gold rush',
            '\'this the damn season',
            'tolerate it',
            'no body, no crime (feat. HAIM)',
            'hapiness',
            'dorothea',
            'coney island (feat. The National)',
            'ivy',
            'cowboy like me',
            'long story short',
            'marjorie',
            'closure',
            'evermore (feat. Bon Iver)',
            'right where you left me - bonus track',
            'it\'s time to go - bonus track',
            'willow',
            'champagne problems',
            'gold rush',
            '\'this the damn season',
            'tolerate it',
            'no body, no crime (feat. HAIM)',
            'hapiness',
            'dorothea',
            'coney island (feat. The National)',
            'ivy',
            'cowboy like me',
            'long story short',
            'marjorie',
            'closure',
            'evermore (feat. Bon Iver)',
            'right where you left me - bonus track',
            'it\'s time to go - bonus track',
          ]
        },
        {
          id: 2,
          name: "lover",
          valor: "150.75",
          year: "2020",
          image_url: 'https://people.com/thmb/vvDOonfXdN5fSqLAioLgg_9AJMY=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc():focal(999x0:1001x2):format(webp)/taylor-swift-lover-2000-e4a62abb38b9483e8d371eda823d2fcb.jpg',
          description: 'Evermore é o nono álbum de estúdio da cantora e compositora estadunidense Taylor Swift. O seu lançamento ocorreu em 11 de dezembro de 2020, através da gravadora Republic Records, menos de cinco meses após Folklore, seu oitavo álbum de estúdio.',
          recorder: 'Republic Records',
          tracks: [
            'willow',
            'champagne problems',
            'gold rush',
            '\'this the damn season',
            'tolerate it',
            'no body, no crime (feat. HAIM)',
            'hapiness',
            'dorothea',
            'coney island (feat. The National)',
            'ivy',
            'cowboy like me',
            'long story short',
            'marjorie',
            'closure',
            'evermore (feat. Bon Iver)',
            'right where you left me - bonus track',
            'it\'s time to go - bonus track',
          ]
        },
        {
          id: 3,
          name: "Taylor Swift",
          valor: "150.75",
          year: "2020",
          image_url: 'https://people.com/thmb/A7_leo8hc_wPis3erIdrtJYVsG8=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc():focal(999x0:1001x2):format(webp)/taylor-swift-albums-1-93026ca98408417097660e117a10a6a9.jpg',
          description: 'Evermore é o nono álbum de estúdio da cantora e compositora estadunidense Taylor Swift. O seu lançamento ocorreu em 11 de dezembro de 2020, através da gravadora Republic Records, menos de cinco meses após Folklore, seu oitavo álbum de estúdio.',
          recorder: 'Republic Records',
          tracks: [
            'willow',
            'champagne problems',
            'gold rush',
            '\'this the damn season',
            'tolerate it',
            'no body, no crime (feat. HAIM)',
            'hapiness',
            'dorothea',
            'coney island (feat. The National)',
            'ivy',
            'cowboy like me',
            'long story short',
            'marjorie',
            'closure',
            'evermore (feat. Bon Iver)',
            'right where you left me - bonus track',
            'it\'s time to go - bonus track',
          ]
        },
        {
          id: 4,
          name: "Reputation",
          valor: "150.75",
          year: "2020",
          image_url: 'https://people.com/thmb/DWnqc5Gyvvo0-YQnqNT11rZSqzQ=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc():focal(992x0:994x2):format(webp)/taylor-swift7-2000-48f9bfb372c34e36866773b1ede0b372.jpg',
          description: 'Evermore é o nono álbum de estúdio da cantora e compositora estadunidense Taylor Swift. O seu lançamento ocorreu em 11 de dezembro de 2020, através da gravadora Republic Records, menos de cinco meses após Folklore, seu oitavo álbum de estúdio.',
          recorder: 'Republic Records',
          tracks: [
            'willow',
            'champagne problems',
            'gold rush',
            '\'this the damn season',
            'tolerate it',
            'no body, no crime (feat. HAIM)',
            'hapiness',
            'dorothea',
            'coney island (feat. The National)',
            'ivy',
            'cowboy like me',
            'long story short',
            'marjorie',
            'closure',
            'evermore (feat. Bon Iver)',
            'right where you left me - bonus track',
            'it\'s time to go - bonus track',
          ]
        }
      ],
      backgroundMapper: {
        'taylor swift': 'taylor-swift-background-color',
        'fearless': 'fearless-background-color',
        'speak now': 'speak-now-background-color',
        'red': 'red-background-color',
        '1989': 'nineteen-eighty-nine-background-color',
        'reputation': 'reputation-background-color',
        'lover': 'lover-background-color',
        'folklore': 'folklore-background-color',
        'evermore': 'evermore-background-color',
        'midnights': 'midnights-background-color'
      }
    }
  },
  methods: {
    nextAlbum() {
      if(this.index === this.albums.length -1) {
        this.index = 0;
      } else this.index++;
    },
    previousAlbum() {
      if(this.index === 0) {
        this.index = this.albums.length - 1;
      } else this.index--;
    }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Rubik");
html,
body {
  height: 100vh;
  width: 100vw;
  margin: 0;
}

#app {
  height: inherit;
  font-family: "Rubik";
  width: inherit;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.taylor-swift-background-color {
  background: rgb(13, 180, 222);
  background: radial-gradient(circle, rgba(13, 180, 222, 1) 0%, rgba(45, 198, 83, 1) 100%);
}

.fearless-background-color {
  background: rgb(236, 206, 117);
  background: radial-gradient(circle, rgba(236, 206, 117, 1) 0%, rgba(145, 108, 57, 1) 100%);
}

.speak-now-background-color {
  background: rgb(178, 152, 220);
  background: radial-gradient(circle, rgba(178, 152, 220, 1) 0%, rgba(151, 58, 168, 1) 100%);
}

.red-background-color {
  background: rgb(237, 72, 57);
  background: radial-gradient(circle, rgba(237, 72, 57, 1) 0%, rgba(202, 15, 46, 1) 100%);
}

.nineteen-eighty-nine-background-color {
  background: rgb(237, 224, 212);
  background: radial-gradient(circle, rgba(237, 224, 212, 1) 0%, rgba(144, 224, 239, 1) 85%);
}

.reputation-background-color {
  background: rgb(108, 117, 125);
  background: radial-gradient(circle, rgba(108, 117, 125, 1) 0%, rgba(0, 0, 0, 1) 100%);
}

.lover-background-color {
  background: rgb(238, 174, 202);
  background: radial-gradient(circle, rgba(238, 174, 202, 1) 0%, rgba(148, 187, 233, 1) 100%);
}

.folklore-background-color {
  background: rgb(167, 147, 130);
  background: radial-gradient(circle, rgba(167, 147, 130, 1) 0%, rgba(173, 181, 189, 1) 100%);
}

.evermore-background-color {
  background: rgb(229, 147, 95);
  background: radial-gradient(circle, rgba(229, 147, 95, 1) 0%, rgba(106, 69, 46, 1) 100%);
}

.midnights-background-color {
  background: rgb(118, 146, 167);
  background: radial-gradient(circle, rgba(118, 146, 167, 1) 0%, rgba(2, 9, 35, 1) 100%);
}

.image-size {
  max-width: 100%;
  height: 100%;
}

.main-row-position {
  padding-top: 50px
}
.detail-album-image {
  cursor: pointer;
  position: absolute;
  top: 0;
  left: 50;
}
.detail-album-image:hover {
  transform: scale(1.2);
  filter: grayscale(20%) brightness(0.3)
}
.detail-album-content {
  position: absolute;
  top: 0;
  left: 40;
  width: 85%;
  max-height: 100%;
  transform: scale(1.2);
  color: white;
  font-size: 11px;
}
.align-text {
  text-align: justify;
  text-justify: inter-character
}
</style>
