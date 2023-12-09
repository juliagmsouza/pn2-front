<template>
  <div :class="backgroundMapper[selectedAlbum.name.toLowerCase()]" id="app">
    <div>
    <b-carousel controls no-animation>
      <b-carousel-slide v-for="(album, index) in albums" :key="index" :img-src="album.image_url" class="aa">
      </b-carousel-slide>
    </b-carousel>
  </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      selectedAlbum: {
        name: 'lover'
      },
      albums: [
        {
          id: 2,
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
          ]
        },
        {
          id: 2,
          name: "evermore",
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
  }
}
</script>

<style>
html,
body {
  height: 100vh;
  width: 100vw;
  margin: 0;
}

#app {
  height: inherit;
  width: inherit;
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
  background: rgb(229,147,95);
  background: radial-gradient(circle, rgba(229,147,95,1) 0%, rgba(106,69,46,1) 100%);
}

.midnights-background-color {
  background: rgb(118, 146, 167);
  background: radial-gradient(circle, rgba(118, 146, 167, 1) 0%, rgba(2, 9, 35, 1) 100%);
}
.aa {
  max-width: 500px;
  max-height: 700px;
}

</style>
