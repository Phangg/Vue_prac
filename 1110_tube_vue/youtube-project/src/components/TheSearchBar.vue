<template>
  <div>
    <input 
      class="form-control"
      type="text"
      v-model="inputData"
      @keyup.enter="sendData"  
    >
  </div>
</template>

<script>
export default {
  name: 'TheSearchBar',
  data() {
    return {
      inputData: null,
    }
  },
  methods: {
    sendData() {
      this.$emit('send-data', this.inputData)
    },
  },
  props: {
    msg: {
      type: String,
    }
  },
  watch: {
    msg() {
      this.inputData = this.msg
    }
  },
}
</script>

<style>

</style>