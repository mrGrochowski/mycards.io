<template>
  <div class="container">
    SOMETHING

    <h1 class="title">Scan 1D/2D Code from Video Camera</h1>

    <div>
      <a class="button" ref="startButton">Start</a>
      <a class="button" ref="resetButton">Reset</a>
    </div>

    <div>
      <video id="video" ref="video" width="300" height="200" style="border: 1px solid gray"></video>
    </div>

    <div ref="sourceSelectPanel">
      <label for="sourceSelect">Change video source:</label>
      <select id="sourceSelect" ref="sourceSelect" style="max-width: 400px"></select>
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

const codeReader = new BrowserMultiFormatReader()

const sourceSelect = ref(null)
const startButton = ref(null)
const resetButton = ref(null)
const video = ref(null)
const resultV = ref(null)

let selectedDeviceId
console.clear()
onMounted(() => {
  codeReader
    .listVideoInputDevices()
    .then((videoInputDevices) => {
      const sourceSelectV = sourceSelect.value
      selectedDeviceId = videoInputDevices[0].deviceId
      if (videoInputDevices.length >= 1) {
        videoInputDevices.forEach((element) => {
          const sourceOption = document.createElement('option')
          sourceOption.text = element.label
          sourceOption.value = element.deviceId
          sourceSelectV.appendChild(sourceOption)
        })

        sourceSelectV.onchange = () => {
          selectedDeviceId = sourceSelect.value
        }

      }

      startButton.value.addEventListener('click', () => {
        codeReader.decodeFromVideoDevice(selectedDeviceId, 'video', (result, err) => {
          if (result) {
            //resultV.value.textContent = result.text
            resultV.value.textContent = result
          }
          // if (err) {
          //   console.error(err)
          //   resultV.value.textContent = err
          // }
        })
        console.log(`Started continous decode from camera with id ${selectedDeviceId}`)
      })

      resetButton.value.addEventListener('click', () => {
        codeReader.reset()
        result.textContent = ''
        console.log('Reset.')
      })
    })
    .catch((err) => {
      console.error(err)
    })
})
</script>

<style scoped>
.container {
  display: inline-block;
}
</style>
