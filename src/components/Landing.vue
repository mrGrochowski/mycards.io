<template>
    <ScannerWrapper></ScannerWrapper>
</template>

<script setup>
import { defineProps, reactive } from 'vue'
import ScannerWrapper from './ScannerWrapper.vue'

defineProps({
  msg: String,
})

const state = reactive({ count: 0 })
</script>
