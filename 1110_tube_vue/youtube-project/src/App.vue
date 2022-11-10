<template>
  <div id="app" class="container">
    <h1 class="Miw changepointer" @click="home">파-ㅇ의 류튜우-브</h1>
    <br>
    <div class="row">
      <TheSearchBar @send-data="searchData" :msg="message"/>
    </div>
    <br>
    <div class="row">
      <div class="col" v-if="selectedVideo">
        <VideoDetail :selectedVideo="selectedVideo"/>
      </div>
      <div class="col">
        <VideoList :videos="videos" @this-video="goVideoDetail"/>
      </div>
    </div>
  </div>
</template>

<script>
import VideoList from "@/components/VideoList"
import VideoDetail from "@/components/VideoDetail"
import TheSearchBar from "@/components/TheSearchBar"
import axios from "axios"
const API_URL='https://www.googleapis.com/youtube/v3/search'
const API_KEY=process.env.VUE_APP_YOUTUBE_API

export default {
  name: 'App',
  components: {
    VideoList,
    VideoDetail,
    TheSearchBar,
  },
  data() {
    return {
      videosList: [],      
      videos: [],
      selectedVideo: null,
      message: null,
    }
  },
  methods: {
    searchData(inputData) {
      console.log(API_KEY)
      // console.log(inputData)
      this.selectedVideo = null
      this.message = inputData
      const params = {
        key: API_KEY,
        part: 'snippet',
        type: 'video',
        q: inputData,
      }
      axios({
        method: 'get',
        url: API_URL,
        params,
      })
        .then((res) => {
          // console.log(res)
          this.videos = res.data.items
        })
        .catch((error) => {
          console.log(error)
        })
    },
    goVideoDetail(video) {
      this.selectedVideo = video
    },
    home() {
      this.selectedVideo = null
      this.videos = this.videosList
      this.message = null
    },
  },
  created() {
    const params = {
      key: API_KEY,
      part: 'snippet',
      type: 'video',
      chart: 'mostPopular',
      regionCode: 'KR',
      videoCategoryId: '10', 
    }
    axios({
      method: 'get',
      url: "https://www.googleapis.com/youtube/v3/videos",
      params,
    })
      .then((res) => {
        // console.log(res)
        this.videos = res.data.items
        this.videosList = res.data.items
      })
      .catch((error) => {
        console.log(error)
      })
  },
}
</script>

<style>

@font-face {
  font-family: "Miw";
  src: url("../Miwon.otf") format("truetype");
}

#app {
  font-family: Miw, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #111010;
  margin-top: 60px;
}

.Miw {
  font-family: Miw, sans-serif;
  color: #d11111;
}

.changepointer {
  cursor: pointer;
}

</style>
