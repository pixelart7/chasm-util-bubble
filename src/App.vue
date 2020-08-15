<template lang="pug">
.app
  Bubble(:value="text")
  input.mt-4.rounded.border.border-gray-300.bg-gray-100(type="text" v-model="text")
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

import Bubble from '@/components/Bubble.vue';

const App = defineComponent({
  components: {
    Bubble,
  },
  setup() {
    const text = ref('Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam mauris elit, interdum in urna cursus, congue blandit quam. Ut ultricies diam ex, vitae auctor tellus rutrum sed. Vivamus porttitor lobortis hendrerit.');

    return {
      text,
    };
  },
});

export default App;
</script>

<style lang="scss">
// .app {}
</style>
