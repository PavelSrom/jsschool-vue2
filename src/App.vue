<template>
  <div class="max-w-xl mx-auto">
    <Navbar />
    <router-view />
  </div>
</template>

<script>
  import Navbar from './components/Navbar';

  export default {
    components: {
      Navbar,
    },
  };
</script>

<style>
  body {
    background: #f2f2f2;
  }
</style>
