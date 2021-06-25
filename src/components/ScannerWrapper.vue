<template>
  <div class="container">
    SOMETHING

    <h1 class="title">Scan 1D/2D Code from Video Camera</h1>

    <div>
      <a class="button" ref="startButton">Start</a>
      <a class="button" ref="resetButton">Reset</a>
    </div>

    <div>
      <video
        id="video"
        ref="videoV"
        width="300"
        height="200"
        style="border: 1px solid gray"
      ></video>
    </div>

    <label>Result:</label>
    <code ref="resultV"></code>

    <p>
      See the
      <a href="https://github.com/zxing-js/library/tree/master/docs/examples/multi-camera/"
        >source code</a
      >
      for this example.
    </p>
  </div>
</template>

<script setup>
import { BrowserMultiFormatReader, BarcodeFormat } from '@zxing/library'
import { ref, onMounted } from 'vue'

const startButton = ref(null)
const resetButton = ref(null)
const videoV = ref(null)
const resultV = ref(null)

const codeReader = new BrowserMultiFormatReader()

let selectedDeviceId
onMounted(() => {
  startButton.value.addEventListener('click', () => {
    codeReader.decodeFromVideoDevice('', videoV.value, (result, err) => {
      if (result) {
        resultV.value.textContent = result
      }
    })
    console.log(`Started continous decode from camera with id ${selectedDeviceId}`)
  })

  resetButton.value.addEventListener('click', () => {
    codeReader.reset()
    result.textContent = ''
    console.log('Reset.')
  })
})
</script>

<style scoped>
.container {
  display: inline-block;
}
</style>
