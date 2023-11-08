<template>
  <div class="wrap" @click="randomIndex.handleWrap">
    <img v-for="item in randomIndex.total" :src="`./img/${item}.jpg`"
      :class="[randomIndex.index.value === item ? 'in' : 'out']">
  </div>

  <!-- <audio src="./1.mp3" autoplay loop ref="mp3"></audio> -->
</template>

<script setup>
import { ref, onMounted } from 'vue'
// let mp3 = ref(null)

// onMounted(() => {
//   mp3.value.play()
// })

class RandomIndex {
  index = ref(1)
  fixed = false
  total = 31
  gap = 5000
  timer = null

  constructor() {
    this.startTimer()
  }

  startTimer() {
    this.timer = setInterval(() => {
      this.index.value = Math.ceil(Math.random() * this.total)
    }, this.gap)
  }

  stopTimer() {
    clearInterval(this.timer)
  }

  handleWrap() {
    // mp3.value.play()

    this.fixed = !this.fixed
    if (this.fixed) {
      this.index.value = 1
      this.timer && this.stopTimer()
    } else {
      this.index.value = Math.ceil(Math.random() * this.total)
      this.timer && this.stopTimer()
      this.startTimer()
    }
  }
}
const randomIndex = new RandomIndex()
console.log('randomIndex: ', randomIndex);

</script>


<style scoped>
.wrap {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;

}

img {
  position: absolute;
  object-fit: contain;
  width: 80%;
  height: 80%;
}

.in,
.out {
  transition: all 0.3s;
}

.in {
  opacity: 1;
}

.out {
  opacity: 0;
}
</style>
