<template>
  <div v-if="selectedVideo">
    <iframe
      :src="selectedVideoUrl"
      frameborder="0"
      width="640" height="360"
    >
    </iframe>
    <h2>
      {{ videoTitle }}
    </h2>
    <hr>
    <h4>
      {{ videoChannelTitle }}
    </h4>
    <p>
      {{ videoDescription }}
    </p>
  </div>
</template>

<script>
import _ from "lodash"

export default {
  name: 'VideoDetail',
  props: {
    selectedVideo: {
      type: Object,
    },
  },
  computed: {
    selectedVideoUrl() {
      if (this.selectedVideo.id.videoId) {
        const videoId = this.selectedVideo.id.videoId
        return `https://www.youtube.com/embed/${videoId}`
      } else {
        const videoId = this.selectedVideo.id
        return `https://www.youtube.com/embed/${videoId}`
      }
    },
    videoTitle() {
      return _.unescape(this.selectedVideo.snippet.title)
    },
    videoDescription() {
      return _.unescape(this.selectedVideo.snippet.description)
    },
    videoChannelTitle() {
      return _.unescape(this.selectedVideo.snippet.channelTitle)
    },
  },
}
</script>

<style>

</style>