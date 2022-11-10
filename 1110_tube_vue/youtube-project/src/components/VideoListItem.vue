<template>
  <li class="list-group-item d-flex align-items-start">
    <img :src="videoUrl" alt="썸네일 이미지" class="me-3 changepointer"
      @click="selectVideo"
    >
    <span @click="selectVideo" class="changepointer text-start">
      {{ videoTitle }}
    </span>
  </li>
</template>

<script>
import _ from "lodash"

export default {
  name: 'VideoListItem',
  props: {
    video: {
      type: Object,
    }
  },
  data() {
    return {
      videoUrl: this.video.snippet.thumbnails.default.url,
      videoTitle: _.unescape(this.video.snippet.title),
    }
  },
  methods: {
    selectVideo() {
      this.$emit('select-video', this.video)
    },
  },
}
</script>

<style>

</style>