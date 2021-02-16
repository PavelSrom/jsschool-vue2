<template>
  <nav class="mb-16 space-x-4 p-2 font-normal text-xl">
    <router-link :to="{ name: 'Home' }">Projects</router-link>
    <router-link :to="{ name: 'AddProject' }">New project</router-link>
  </nav>
</template>

<style scoped>
  a.router-link-active {
    border-bottom: 2px solid deepskyblue;
  }
</style>
