<template lang="pug">
.bubble.overflow-hidden.border.border-gray-400.rounded-lg(ref="bubble" :style="styleString")
  p.text-center.word-break {{text}}
</template>

<script lang="ts">
import {
  defineComponent, onMounted, ref, computed, nextTick, watch,
} from 'vue';

function isTruncated(el: Element) {
  console.log('el.scrollWidth', el.scrollWidth);
  console.log('el.clientWidth', el.clientWidth);
  console.log('el.scrollHeight', el.scrollHeight);
  console.log('el.clientHeight', el.clientHeight);
  return el.scrollWidth > el.clientWidth || el.scrollHeight > el.clientHeight;
}

const MAX_SIZE = 512;

const App = defineComponent({
  props: {
    value: {
      type: String,
      default: '',
    },
  },
  setup(props) {
    const text = computed(() => props.value);
    const size = ref(24);
    const bubble = ref(null);

    const styleString = computed(() => `width: ${size.value}px; height: ${size.value}px;`);

    function onTextChange() {
      if (bubble.value) {
        if (isTruncated(bubble.value as unknown as Element)) {
          nextTick(() => { size.value += 1; onTextChange(); });
        }
      }
    }

    watch(text, () => { size.value = 24; nextTick(() => { onTextChange(); }); });
    onMounted(() => { onTextChange(); });

    return {
      text,
      styleString,
      bubble,
    };
  },
});

export default App;
</script>

<style lang="scss">
// .app {}
</style>
