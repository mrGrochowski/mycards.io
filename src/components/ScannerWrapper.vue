<template>
  <div class="relative h-screen w-screen flex justify-center items-center">
    <video
      ref="videoV"
      class="h-screen z-0 w-screen absolute select-none pointer-events-none object-cover"
    ></video>
    <div
      class="
        inline-flex w-3/4 h-4/6 sm:h-1/2 sm:w-1/2
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

<script>
import {setBase , writeToBase, getFromBase} from "../composables/storage.vue"
import { BrowserMultiFormatReader } from '@zxing/library'
import { ref, onMounted } from 'vue'

const startScanning = (codeReader, videoV, resultV) => {
  codeReader.decodeFromVideoDevice('', videoV, (result, err) => {
    if (result) {
      resultV.textContent = result.text
    }
  })
}

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

    setBase()
    //writeToBase()
    getFromBase()
    onMounted(()=>{


      //callStartScanning()
    })
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
.container {
  display: inline-block;
}
</style>
