<template>
  <div>
    <p v-if="!imgsrc">{{ message }}</p>
    <img :src="imgsrc" alt="">
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'DogView',
  data() {
    return{
      imgsrc: null,
      message: '로딩 중...',
    }
  },
  methods: {
    getDogImage() {
      const breed = this.$route.params.breed
      const dogImageUrl = `https://dog.ceo/api/breed/${breed}/images/random`

      axios({
        method: 'get',
        url: dogImageUrl,
      })
        .then((response) => {
          console.log(response)
          const imgsrc = response.data.message
          this.imgsrc = imgsrc
        }) 
        .catch((error) => {
          // this.message = `${this.$route.params.breed}는 없는 품종입니다.`
          this.$router.push('/404')
          console.log(error)
        })
    }
  }, 
  created() {
    this.getDogImage()
  }
}
</script>

<style>

</style>