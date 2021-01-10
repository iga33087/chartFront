<template>
  <div class="home">
    <ChartBox v-for="(item,index) in memberList" :memberId="item" :key="index" />
  </div>
</template>

<script>
// @ is an alias to /src
import ChartBox from '@/components/ChartBox.vue'

export default {
  name: 'Home',
  components: {
    ChartBox
  },
  data() {
    return {
      memberList:[]
    }
  },
  sockets: {
    member: function (x) {
      console.log(x)
      this.memberList=x
    },
  },
}
</script>
