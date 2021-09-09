<template>
  <v-container class="mt-10">
    <v-row>
      <v-col cols="4">
        <FormTask @taskCreated="getAllTasks" />
      </v-col>
      <v-col cols="8">
        <div v-for="(task, index) in tasks" :key="index" class="mb-4">
          <ListTask
            :id="task._id"
            :title="task.title"
            :description="task.description"
            @taskDeleted="getAllTasks"
          />
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import FormTask from "@/components/FormTask.vue";
import ListTask from "@/components/ListTask.vue";
export default {
  components: { FormTask, ListTask },
  data() {
    return {
      tasks: [],
    };
  },
  mounted() {
    this.getAllTasks();
  },
  methods: {
    async getAllTasks() {
      const hostname = "http://localhost:4800/tasks";
      const response = await fetch(hostname + "/get/all");
      const tasks = await response.json();
      this.tasks = tasks;
    },
  },
};
</script>
