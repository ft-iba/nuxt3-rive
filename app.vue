<script setup lang="ts">
import { onMounted, onUnmounted, ref, watch } from 'vue';
import RiveItem from './components/RiveItem.vue';

const riveItem = ref<InstanceType<typeof RiveItem> | null>(null);
const riveLoaded = ref<boolean>(false);

const onLoadRiveItem = () => {
  console.log('onLoadRiveItem');
  riveLoaded.value = true;
}

const onPlayRiveItem = () => {
  console.log('onPlayRiveItem');
  riveItem.value?.onPlay();
}

onMounted(async() => {
  console.log('onMounted');
  if (!riveItem.value) return;
  if (riveLoaded.value && riveItem.value) {
    onPlayRiveItem();
  }
  // await new Promise(resolve => setTimeout(resolve, 400));
});

onUnmounted(() => {
});

watch(riveLoaded, (loaded) => {
  if (loaded && riveItem.value) {
    onPlayRiveItem();
  }
});
</script>

<template>
  <div>
    <RiveItem
      ref="riveItem"
      @loaded="onLoadRiveItem"
    />
  </div>
</template>

<style>
html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
abbr, address, cite, code,
del, dfn, em, img, ins, kbd, q, samp,
small, strong, sub, sup, var,
b, i,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, figcaption, figure,
footer, header, hgroup, menu, nav, section, summary,
time, mark, audio, video {
  margin:0;
  padding:0;
  border:0;
  outline:0;
  font-size:100%;
  vertical-align:baseline;
  background:transparent;
}
</style>
