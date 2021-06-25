<template>
<div
    class="
      min-h-screen
      flex flex-shrink-0 flex-grow-0 flex-col
      justify-center
      items-center
      bg-gradient-to-r
      from-gray-600
      to-gray-500
    "
  >
    <a
      @click="callStartScanning"
      class="
        bg-blue-500
        rounded-lg
        font-bold
        text-white text-center
        px-4
        py-3
        transition
        duration-300
        ease-in-out
        hover:bg-blue-600
      "
    >
      Dodaj pierwszą kartę
    </a>
    <a
      @click="callResetScanning"
      class="
        bg-blue-800
        rounded-lg
        font-bold
        text-white text-center
        px-4
        py-3
        transition
        duration-300
        ease-in-out
        hover:bg-blue-600
      "
    >
      Resetuj
    </a>
      <video
        ref="videoV"
        class="vid"
      ></video>

    <label>Result:</label>
    <code ref="resultV"></code>

  </div>
</template>

<script>
import { BrowserMultiFormatReader } from '@zxing/library'
import { ref, onMounted } from 'vue'

const startScanning = (codeReader, videoV, resultV) => {

  codeReader.decodeFromVideoDevice('', videoV, (result, err) => {
    if (result) {
      resultV.textContent = result.text
    }
  })
  console.log(`Started continous decode from camera with id `)

}

const resetScanning = (codeReader, resultV) => {
  console.log(resultV)
  codeReader.reset()
  resultV.textContent = ''
  console.log('Reset.')

}
export default {
  setup() {
    const videoV = ref(null)
    const resultV = ref(null)
    const codeReader = new BrowserMultiFormatReader()

    const callStartScanning = ()=> startScanning(codeReader, videoV.value, resultV.value)
    const callResetScanning = ()=> resetScanning(codeReader, resultV.value)

    return {
      callStartScanning,
      callResetScanning,
      videoV,resultV
    }
  },
}
</script>

<style scoped>
.container {
  display: inline-block;
}

.vid {
  width:50vw;
  height:50vh
}
</style>
