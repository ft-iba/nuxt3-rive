<script setup lang="ts">
import { onMounted, onUnmounted, ref, defineExpose } from 'vue';
import { Rive } from '@rive-app/canvas';

const node = ref<HTMLCanvasElement | null>(null);
let riveInstance: Rive | null = null;
let resizeObserver: ResizeObserver | null = null;
let resizeThrottleTimer: number | null = null;
const throttleDelay = 100; // ms

const emit = defineEmits<{
  loaded: []
}>();

const onLoad = () => {
  console.log('onLoad');
  emit('loaded');
};

const onPlay = () => {
  console.log('onPlay');
  riveInstance?.play();
};

const onResizeDraw = () => {
  console.log('onResizeDraw');
  riveInstance?.resizeDrawingSurfaceToCanvas();
};

onMounted(() => {
  if (!node.value) return;

  riveInstance = new Rive({
    src: 'https://cdn.rive.app/animations/vehicles.riv',
    canvas: node.value,
    autoplay: false,
    stateMachines: 'bumpy',
    onLoad: onLoad,
  });

  resizeObserver = new ResizeObserver((entries: ResizeObserverEntry[]) => {
    if (!entries.length || !node.value) return;

    const contentRect = entries[0].contentRect;
    const canvas = node.value;

    const dpr = window.devicePixelRatio || 1;
    const expectedWidth = Math.round(contentRect.width * dpr);
    const expectedHeight = Math.round(contentRect.height * dpr);

    const isSizeEqual =
      canvas.width === expectedWidth &&
      canvas.height === expectedHeight;

    if (isSizeEqual) return;

    if (resizeThrottleTimer !== null) return;

    resizeThrottleTimer = window.setTimeout(() => {
      resizeThrottleTimer = null;
      console.log('resizeObserver');
      onResizeDraw();
    }, throttleDelay);
  });

  resizeObserver.observe(node.value);
});

onUnmounted(() => {
  riveInstance?.cleanup();
  resizeObserver?.disconnect();
  if (resizeThrottleTimer !== null) {
    clearTimeout(resizeThrottleTimer);
  }
});

defineExpose({
  onPlay
});
</script>

<template>
  <canvas
    ref="node"
    class="canvas"
  />
</template>

<style>
.canvas {
  height: auto;
  width: 100%;
}
</style>
