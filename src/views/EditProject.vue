<template>
  <div>
    <h1 class="text-3xl font-semibold mb-8">Edit project</h1>

    <form v-if="!!project" @submit.prevent="handleSubmit" class="flex flex-col">
      <label for="title">Title</label>
      <input
        type="text"
        required
        v-model="project.title"
        class="mb-4 p-2 rounded-md"
      />
      <label for="details">Details</label>
      <textarea
        required
        v-model="project.details"
        class="mb-4 p-2 rounded-md overflow-hidden resize-none"
      ></textarea>

      <button
        class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-yellow-600 hover:bg-yellow-700 md:py-4 md:text-lg md:px-10"
      >
        Edit project
      </button>
    </form>
  </div>
</template>

<script>
  export default {
    data: () => ({
      project: null,
    }),
    async mounted() {
      const id = this.$route.params.id;

      try {
        const response = await fetch(`http://localhost:3000/projects/${id}`);
        const data = await response.json();

        this.project = data;
      } catch (err) {
        console.log(err);
      }
    },
    methods: {
      async handleSubmit() {
        const id = this.$route.params.id;
        const body = JSON.stringify(this.project);

        try {
          await fetch(`http://localhost:3000/projects/${id}`, {
            method: 'PATCH',
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
