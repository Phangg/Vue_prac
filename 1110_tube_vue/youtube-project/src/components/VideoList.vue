<template>
  <div>
    <ul class="list-group">
      <VideoListItem 
        v-for="video in videos"
        :key="video.id.videoId"
        :video="video"
        @select-video="thisVideo"
      />
    </ul>
  </div>
</template>

<script>
import VideoListItem from "@/components/VideoListItem"

export default {
  name: 'VideoList',
  components: {
    VideoListItem,
  },
  props: {
    videos: {
      type: Array,
      // required: true,
    }
  },
  methods: {
    thisVideo(video) {
      this.$emit('this-video', video)
    },
  },
}
</script>

<style>

</style>