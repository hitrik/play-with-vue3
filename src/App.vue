<template>
  <div id="app">
    <data-loader :request="requestRemoteData">
      <template #default="{ loading, response, triggerRequest }">
        <DataConsumer :renderData="response" :triggerRequest="triggerRequest" />
      </template>
      <template #skeleton>
        <div>Skeleton is blinking...</div>
      </template>
      <template #error="{ error }">
        <div class="error">Error: {{ error }}</div>
      </template>
    </data-loader>
  </div>
</template>

<script>
import DataConsumer from './components/DataConsumer.vue';
import DataLoader from './components/DataLoader.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  components: {
    DataConsumer,
    DataLoader,
  },

  setup() {
    const requestRemoteData = () => {
      return fetch('https://jsonplaceholder.typicode.com/todos/1').then(
        (response) => response.json()
      );
    };

    return {
      requestRemoteData,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.error {
  color: tomato;
}
</style>
