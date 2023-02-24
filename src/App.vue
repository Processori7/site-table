<template>
  <v-app>
    <v-main>
      <HelloWorld/>
      <Tree_objects/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Tree_objects from './components/Tree_objects';

export default {
  name: 'App',

  components: {
    HelloWorld,
    Tree_objects,
  },

  data: () => ({
    //
  }),
};
</script>
