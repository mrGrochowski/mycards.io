<template>
  <div class="relative h-screen w-screen flex justify-center items-center">
    <video
      ref="videoV"
      class="h-screen z-0 w-screen absolute select-none pointer-events-none object-cover"
    ></video>
    <div
      class="
        inline-flex w-3/4 h-4/4
        flex-shrink-0 flex-grow-0 flex-wrap
        justify-center
        items-center
        z-10
        relative
        p-9
        rounded-lg
        specialGradient
      "
    >
      <h2 class="text-white text-4xl">Skan karty</h2>
      <a
        @click="callStartScanning"
        class="
          bg-blue-600
          rounded-lg
          font-bold
          text-white text-center
          px-4
          py-3
          transition
          duration-300
          ease-in-out
          hover:bg-blue-700
        "
      >
        Dodaj pierwszą kartę
      </a>
      <a
        @click="callResetScanning"
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
        Resetuj
      </a>
      <div class="align-bottom justify-end w-auto min-w-3/4 h-16 p-4">
        <label>Result:</label>
        <code class="w-2/3 inline-block" ref="resultV"></code>
      </div>
    </div>
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
  codeReader.reset()
  resultV.textContent = ''
}
export default {
  setup() {
    const videoV = ref(null)
    const resultV = ref(null)
    const codeReader = new BrowserMultiFormatReader()

    const callStartScanning = () => startScanning(codeReader, videoV.value, resultV.value)
    const callResetScanning = () => resetScanning(codeReader, resultV.value)

    return {
      callStartScanning,
      callResetScanning,
      videoV,
      resultV,
    }
  },
}
</script>

<style scoped>
.z--1 {
  z-index: -1;
}
.specialGradient {
  background: linear-gradient(
    43deg,
    rgba(55, 59, 68, 0.432) 30%,
    rgba(153, 150, 201, 0.342) 100%
  );
  backdrop-filter: blur(10px);
  box-shadow: 0px 0px 40px rgba(67, 65, 87, 0.63);
}
</style>
