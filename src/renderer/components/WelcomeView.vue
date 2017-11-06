<template>
  <v-container fluid grid-list-md>
    <v-layout row wrap>
      <v-flex
        xs2
        v-for="image in images"
        :key="image.id"
        @click="loadImage(image)"
      >
        <v-card flat tile>
          <v-card-media
            :src="image.previewUrl"
            height="200px"
          >
          </v-card-media>
        </v-card>
      </v-flex>
      <v-dialog v-model="dialog" max-height=1080 max-width=1920>
        <v-card flat tile>
          <v-card-media
            :src="currentImage.url"
            height=725
          >
          </v-card-media>
        </v-card>
      </v-dialog>
    </v-layout>
  </v-container>
</template>

<script>
  var Mousetrap = require('mousetrap')
  export default {
    name: 'welcome',
    methods: {
      loadImage (image) {
        let img = new Image()
        img.src = image.url
        img.addEventListener('load', () => {
          this.currentImage = image
          this.dialog = true
        })
      },
      onChangeImage (val) {
        if (this.dialog) {
          let nextImageIndex = (this.currentImage.id + val) < 0
            ? (this.images.length + val) % this.images.length
            : (this.currentImage.id + val) % this.images.length
          this.loadImage(this.images[nextImageIndex])
        }
      },
      loadImages () {
        for (var index = 0; index < 84; index++) {
          this.images.push({
            id: index,
            url: 'https://unsplash.it/1920/1080?image=' + index,
            previewUrl: 'https://unsplash.it/200?image=' + index
          })
        }
      }
    },
    data: () => ({
      dialog: false,
      currentImage: {},
      images: []
    }),
    mounted () {
      Mousetrap.bind('left', () => this.onChangeImage(-1), 'keyup')
      Mousetrap.bind('right', () => this.onChangeImage(1), 'keyup')
      this.loadImages()
    }
  }
</script>
