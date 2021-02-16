<template>
  <div>
    <div class="flex space-x-4 cursor-pointer font-semibold">
      <p @click="tab = 0">All</p>
      <p @click="tab = 1">Completed</p>
      <p @click="tab = 2">Ongoing</p>
    </div>

    <div v-if="projectsToShow.length" class="space-y-4 mt-10">
      <SingleProject
        v-for="project in projectsToShow"
        :key="project.id"
        :project="project"
        @onDone="handleDone"
        @onDelete="handleDelete"
      />
    </div>
    <p v-else class="mt-10">No projects to show</p>
  </div>
</template>

<script>
  import SingleProject from '../components/SingleProject';

  export default {
    name: 'Home',
    components: {
      SingleProject,
    },
    data: () => ({
      tab: 0,
      projects: [],
    }),
    computed: {
      projectsToShow() {
        if (this.tab === 1)
          return this.projects.filter(({ completed }) => completed);
        if (this.tab === 2)
          return this.projects.filter(({ completed }) => !completed);

        return this.projects;
      },
    },
    methods: {
      handleDone(id) {
        const targetIndex = this.projects.findIndex(proj => proj.id === id);
        this.projects[targetIndex].completed = !this.projects[targetIndex]
          .completed;
      },
      handleDelete(id) {
        this.projects = this.projects.filter(proj => proj.id !== id);
      },
    },
    async mounted() {
      try {
        const response = await fetch('http://localhost:3000/projects');
        const data = await response.json();

        this.projects = data;
      } catch (err) {
        console.log(err);
      }
    },
  };
</script>
