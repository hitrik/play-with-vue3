<template>
  <slot v-bind="{ error, loading, response, startRequest }"></slot>
</template>

<script>
import { defineComponent, ref, watch } from 'vue';

export default defineComponent({
  name: 'DataLoader',

  props: {
    request: {
      type: Function,
      required: true,
    },
  },

  setup() {
    const response = ref(null);
    const error = ref(null);
    const loading = ref(false);

    const trigger = ref(false);
    const startRequest = () => {
      trigger.value = !trigger.value;
    };

    watch(trigger, () => {
      error.value = null;
      loading.value = true;
      request()
        .then((serverResponse) => {
          response.value = serverResponse;
          console.log(serverResponse);
        })
        .catch((err) => {
          error.value = err;
        })
        .finally(() => {
          loading.value = false;
        });
    });

    return {
      startRequest,
      response,
      loading,
      error,
    };
  },
});
</script>
