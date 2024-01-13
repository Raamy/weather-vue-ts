<template>
  <navigation-bar/>
  <router-view/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import NavigationBar from './components/NavigationBar.vue';

export default defineComponent({
  components: { NavigationBar },
  name: 'App',
});
</script>

<style lang="scss">

</style>
