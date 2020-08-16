<template lang="pug">
.app.p-4
  .mb-2
    p.px-2.font-mono.text-gray-600 <a class="hover:opacity-75" href="https://github.com/pixelart7/chasm-util-bubble/">pixelart7/chasm-util-bubble</a>
    p.px-2.font-mono.text-gray-500.text-xs Built with coffee and webdev love by <a class="underline hover:opacity-75" href="https://pixelart7.github.io/">github/pixelart7 (aka. PIX7)</a>
  .flex
    .flex-1.px-2.py-2
      textarea.p-2.border.border-blue-500.w-full(v-model="textInput" rows="20")
    .flex-1.px-2
      Bubble.my-2(v-for="t in texts" :value="t")
  //- input.mt-4.rounded.border.border-gray-300.bg-gray-100(type="text" v-model="text")
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue';

import Bubble from '@/components/Bubble.vue';

const App = defineComponent({
  components: {
    Bubble,
  },
  setup() {
    const textInput = ref(`Which reminds me: He's sent me to find you.

Your orders are to report to Commander Silxer's office at once.

Maybe then some new customers will come along and try my brews.`);

    const texts = computed(() => textInput.value.replace(/\r/g, '').split(/\n/).filter((t) => t !== ''));

    return {
      textInput,
      texts,
    };
  },
});

export default App;
</script>

<style lang="scss">
// .app {}
</style>
