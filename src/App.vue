<template>
  <div class="container">
    <h1>Timer</h1>
    <div class="time">{{ formatTime(count) }}</div>
    <div class="btns">
      <button v-if="start" @click="startFunc">Start</button>
      <button v-if="stop" @click="stopFunc">Stop</button>
      <button v-if="continue" @click=" continueFunc ">Continue</button>
      <button v-if=" restart " @click=" restartFunc ">Restart</button>
      <button v-if=" save " @click=" saveFunc ">SAVE</button>
    </div>
    <ul>
      <li v-if="save" v-for=" item, index in  score " :key=" item ">
        {{ index + 1 }})
        {{ item }}
      </li>
      <h3 v-else>There are not records!</h3>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      start: true,
      stop: false,
      restart: false,
      continue: false,
      interval: '',
      score: [],
      save: false,
      count: 0,
      fullTime: '',
    }
  },
  methods: {
    startFunc() {
      console.log('start');
      this.start = !this.start
      this.stop = !this.stop
      this.save = !this.save
      this.countInc()
    },
    stopFunc() {
      console.log('pause');
      this.stop = !this.stop
      this.restart = !this.restart
      this.continue = !this.continue
      clearInterval(this.interval)
    },
    restartFunc() {
      console.log('restart');
      this.stop = !this.stop
      this.continue = !this.continue
      this.restart = !this.restart
      this.save = !this.save
      this.count = 0
      this.countInc()
    },
    continueFunc() {
      this.restart = !this.restart
      this.stop = !this.stop
      this.continue = !this.continue
      // this.save = !this.save
      this.countInc()
    },
    countInc() {
      this.interval = setInterval(() => {
        this.count++
      }, 1000)
    },
    formatTime() {
      const minutes = `0${Math.floor(this.count / 60)}`.slice(-2)
      const seconds = `0${this.count % 60}`.slice(-2)
      this.fullTime = `${minutes}:${seconds}`
      return `${minutes}:${seconds}`
    },
    saveFunc() {
      this.score.unshift(this.fullTime)
      if(this.score.length === 6) {
        this.score.pop(this.fullTime)
      }
    }
  }
}
</script>

<style>
ul {
  list-style: none;
}

ul li {
  color: white;
  font-size: 30px;
}

h3 {
  margin-top: 40px;
  font-size: 25px;
  text-decoration: underline;
  color: white;
}
</style>