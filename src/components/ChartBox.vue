<template>
  <div class="chartBox">
    <div class="chartBoxTitle">{{memberId}}</div>
    <div class="chartBoxList">
      <div class="chartBoxListItem" :class="item.side==='admin' ? 'admin':'client'" v-for="(item,index) in msg" :key="index">{{item.text}}</div>
    </div>
    <div class="chartBoxMenu">
      <input type="text" v-model="text" @keyup.enter="snedMsg">
      <button @click="snedMsg">SNED</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg:[],
      text:"",

    }
  },
  props: {
    memberId: {
    }
  },
  created() {
    this.sockets.subscribe(this.memberId,(data)=> {
      this.msg.push(data)
      console.log(data)
    })
  },
  methods: {
    getMsg(e) {
      this.msg.push(e)
      console.log(this.msg)
    },
    snedMsg() {
      if(!this.text) return 0
      let obj={id:this.memberId,text:this.text}
      this.$socket.emit('adminMsg',obj)
      this.text=""
    }
  }
}
</script>
