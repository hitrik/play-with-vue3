<template>
  <template v-if="loading">
    <slot name="skeleton">Skeleton starts to blink....</slot>
  </template>
  <template v-else-if="error">
    <slot name="error" v-bind="{ error }">Error occured</slot>
  </template>
  <template v-else>
    <slot v-bind="{ response, triggerRequest }"></slot>
  </template>
</template>

<script>
import { defineComponent, ref, watch } from 'vue';

const delay = (ms) => new Promise((res) => setTimeout(res, ms));

export default defineComponent({
  name: 'DataLoader',

  props: {
    request: {
      type: Function,
      required: true,
    },
  },

  setup(props) {
    const response = ref(null);
    const error = ref(null);
    const loading = ref(false);

    const trigger = ref(false);

    const triggerRequest = () => {
      trigger.value = !trigger.value;
    };

    watch(trigger, () => {
      error.value = null;
      loading.value = true;

      Promise.all([props.request(), delay(2000)])
        .then((serverResponse) => {
          response.value = serverResponse;
        })
        .catch((err) => {
          error.value = err;
        })
        .finally(() => {
          loading.value = false;
        });
    });

    return {
      triggerRequest,
      response,
      loading,
      error,
    };
  },
});
</script>
