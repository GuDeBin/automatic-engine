<template>
  <!-- <div>Hello World!</div> -->
  <h1>Speech Recognition</h1>
  <p v-if="!isSupported">SpeechRecognition API not supported!</p>
  <p v-if="isSupported && !isListening">Click start to start listening</p>
  <p v-if="isSupported && isListening">Listening...</p>
  <p v-if="isSupported && isFinal">Interim result: {{ result }}</p>
  <p v-if="isSupported && !isFinal">Final result: {{ result }}</p>
  <button @click="start" style="background-color: green; margin: 10px">
    start
  </button>
  <button @click="stop" style="background-color: red; margin: 10px">
    stop
  </button>
</template>

<script setup>
import { useSpeechRecognition } from "@vueuse/core";
// import { watch } from "vue";

const { isSupported, isListening, isFinal, result, start, stop } =
  useSpeechRecognition({
    lang: "cmn-Hans-CN",
  });

if (!isSupported.value) {
  alert("SpeechRecognition API not supported!");
}

// 三十秒不说话自动结束
watch(isListening, (value) => {
  if (value) {
    setTimeout(() => {
      stop();
    }, 30000);
  }
});
</script>
