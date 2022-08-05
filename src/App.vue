<template>
  <div id="app">
    <data-loader :request="helloRequest">
      <template #default="{ loading, error, response, startRequest }">
        <div>
          <div v-if="error">
            {{ error }}
          </div>
          <HelloWorld :msg="response" :start="startRequest" />
        </div>
      </template>
    </data-loader>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import DataLoader from './components/DataLoader.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld,
    DataLoader,
  },

  setup() {
    const helloRequest = () => {
      return fetch('https://jsonplaceholder.typicode.com/todos/1');
    };

    return {
      helloRequest,
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
</style>
