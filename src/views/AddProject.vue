<template>
  <form @submit.prevent="handleSubmit" class="flex flex-col">
    <label for="title">Title</label>
    <input type="text" required v-model="title" class="mb-4 p-2 rounded-md" />
    <label for="details">Details</label>
    <textarea
      required
      v-model="details"
      class="mb-4 p-2 rounded-md overflow-hidden resize-none"
    ></textarea>

    <button
      class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-yellow-600 hover:bg-yellow-700 md:py-4 md:text-lg md:px-10"
    >
      Add project
    </button>
  </form>
</template>

<script>
  import { API_URL } from '../api';

  export default {
    data: () => ({
      title: '',
      details: '',
    }),
    methods: {
      async handleSubmit() {
        const body = JSON.stringify({
          title: this.title,
          details: this.details,
          completed: false,
        });

        try {
          await fetch(API_URL, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body,
          });

          this.$router.push('/');
        } catch (err) {
          console.log(err);
        }
      },
    },
  };
</script>
