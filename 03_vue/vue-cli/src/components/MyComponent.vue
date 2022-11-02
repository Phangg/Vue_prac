// MyComponent.vue

<template>
  <div class='border'>
    <h1>This is my gorgeous component shxx</h1>
    <!-- 3. 보여주기 -->
    <MyChild 
      static-props="MyComponent에서 보낸 정적 데이터" 
      :dynamic-props="dynamicProps"
      @child-to-parent="parentGetEvent"
      @child-input="getDynamicData"
    />
  </div>
</template>

<script>
// 1. 불러오기
import MyChild from '@/components/MyChild'

export default {
  name: 'MyComponent',
  // 2. 등록하기
  components: {
    MyChild,
  }, 
  data: function () {
    return {
      dynamicProps: '이건 동적인 데이터!',
    }
  },
  methods: {
    parentGetEvent: function (inputData) {
      console.log('자식 컴포넌트에서 발생한 emit 이벤트를 들었다!')
      console.log(`자식 컴포넌트로부터 ${inputData}를 받음!`)
    },
    getDynamicData: function (childInputData) {
      console.log(`사용자가 입력한 값은 ${childInputData}입니다.`)
    }
  },
}
</script>

<style>
  .border {
    border: solid 1px black;
  }
</style>