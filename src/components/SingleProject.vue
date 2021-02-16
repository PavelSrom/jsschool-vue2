<template>
  <div
    class="bg-white shadow-lg p-4 border-l-8"
    :class="{
      'border-red-500': !project.completed,
      'border-green-500': project.completed,
    }"
  >
    <div class="flex justify-between items-center">
      <h4
        class="text-green-500 text-2xl font-semibold cursor-pointer truncate"
        @click="toggleShowDetails"
      >
        {{ project.title }}
      </h4>
      <div class="space-x-2 w-24 flex justify-end">
        <span
          class="material-icons cursor-pointer text-gray-400 hover:text-gray-900"
          @click="$router.push(`/projects/${project.id}`)"
        >
          edit
        </span>
        <span
          class="material-icons cursor-pointer text-gray-400 hover:text-gray-900"
          @click="onDelete"
        >
          delete
        </span>
        <span
          class="material-icons cursor-pointer text-gray-400 hover:text-gray-900"
          :class="{ 'text-green-500 font-extrabold': project.completed }"
          @click="toggleComplete"
        >
          done
        </span>
      </div>
    </div>
    <p v-if="showDetails">{{ project.details }}</p>
  </div>
</template>

<script>
  export default {
    props: ['project'],
    data: () => ({
      showDetails: false,
    }),
    methods: {
      toggleShowDetails() {
        this.showDetails = !this.showDetails;
      },
      async onDelete() {
        try {
          await fetch(`http://localhost:3000/projects/${this.project.id}`, {
            method: 'DELETE',
          });

          this.$emit('onDelete', this.project.id);
        } catch (err) {
          console.log(err);
        }
      },
      async toggleComplete() {
        try {
          await fetch(`http://localhost:3000/projects/${this.project.id}`, {
            method: 'PATCH',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ completed: !this.project.completed }),
          });

          this.$emit('onDone', this.project.id);
        } catch (err) {
          console.log(err);
        }
      },
    },
  };
</script>
