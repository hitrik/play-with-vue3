<template>
  <div class="hello">
    <h1>{{ JSON.stringify(msg) }}</h1>
    <p>
      Hello world;
    </p>
    </ul>
  </div>
</template>

<script>
import {defineComponent, onMounted} from 'vue';
export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: {type: String},
    start: {type: Function}
  },

  setup(props) {
    console.log(props);

    onMounted(() => {
      console.log('mounted');
      // props.start();
    });
  }

});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
