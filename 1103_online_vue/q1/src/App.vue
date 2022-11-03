<template>
  <div id="app">
    <h1>버튼 박스 제작</h1>
    <div class="box">
      <h2>예약 페이지</h2>
      <h3>시간 선택</h3>
      <div id="timeTable">
        <div 
          v-for="(time, index) in times" :key="index"
          @click="selectTime"
        >
          {{ time }}
        </div>
      </div>
      <br>
      <hr>
      <p>
        <b>
          선택 시간 : 
          <span v-for="(sTime, index) in selected" :key="index">
            {{ sTime }}
          </span>
        </b>
      </p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function () {
    return {
      times: [
        "09:00","09:30","10:00","10:30","11:00","11:30","12:00","12:30","13:00","13:30",
        "14:00","14:30","15:00","15:30","16:00","16:30","17:00","17:30","18:00","18:30",
        "19:00","19:30","20:00","20:30","21:00","21:30","22:00","22:30","23:00","23:30",
      ],
      selected: [],
    }
  },
  methods: {
    selectTime: function (e) {
      // console.log(e)
      // console.log(e.target.innerText)

      const selectedTime = e.target.innerText
      if (this.selected.includes(selectedTime)) {
        const idx = this.selected.indexOf(selectedTime)
        this.selected.splice(idx, 1)
      } else {
        this.selected.push(selectedTime)
        this.selected.sort()
      }
      if (this.selected.length > 5) {
        alert('5 타임까지만 신청할 수 있습니다.')
        const idx = this.selected.indexOf(selectedTime)
        this.selected.splice(idx, 1)
      } else {
        e.target.classList.toggle("timeBox")
      }
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
	
#timeTable {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(50px,1fr));
  grid-gap: 15px;
  padding: 15px;
}

.box {
  box-shadow: 0 2px 5px #84898c;
  width: 450px;
  margin: auto;
  padding: 10px 0;
}

.timeBox {
  background-color: #799bb98f;
  color: #0F4C81;
}

</style>
