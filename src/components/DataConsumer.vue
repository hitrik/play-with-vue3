<template>
  <div class="consumer">
    <p>Hello, today i've got data from DataLoader component:</p>
    <p>
      {{ JSON.stringify(renderData) }}
    </p>
    <button @click="triggerRequest">triggerRequest manual</button>
  </div>
</template>

<script>
import { defineComponent, onMounted } from 'vue';
export default defineComponent({
  name: 'DataConsumer',
  props: {
    renderData: { type: Object },
    triggerRequest: { type: Function },
  },

  setup(props) {
    onMounted(props.triggerRequest);
  },
});
</script>
