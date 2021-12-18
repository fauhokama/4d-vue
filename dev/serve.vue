<script>
import Vue from 'vue';
import Screen from '@/screen.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    Screen
  }
});
</script>

<template>
  <div id="app">
    <Screen>
      <h1> Hello </h1>
    </Screen>
  </div>
</template>
