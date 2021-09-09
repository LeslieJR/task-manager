<template>
  <v-container>
    <nuxt-link to="/tasks">Home</nuxt-link>
    <v-card>
      <v-card-title>Editar tarea</v-card-title>
      <v-card-text>
        <v-text-field
          label="Titulo"
          clearable
          v-model="task.title"
        ></v-text-field>
        <v-text-field
          label="Descripción"
          clearable
          v-model="task.description"
        ></v-text-field>
        <v-btn style="backgroundcolor: cornflowerblue" block @click="edited"
          >Guardar</v-btn
        >
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  asyncData(ctx) {
    const id = ctx.params.id;

    //el return seria como definir data(){ id } por lo que después podemos tener acceso através del this
    return {
      id,
    };
  },
  data() {
    return {
      task: {},
    };
  },
  mounted() {
    this.getTask();
  },
  methods: {
    async getTask() {
      const hostname = "http://localhost:4800/tasks";
      const res = await fetch(hostname + "/get/" + this.id);
      const task = await res.json();
      this.task = task;
    },
    async edited() {
      const hostname = "http://localhost:4800/tasks";
      const data = {
        title: this.task.title,
        description: this.task.description,
      };
      const res = await fetch(hostname + "/update/" + this.id, {
        method: "put",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      });
      this.$router.push('/tasks')
    },
  },
};
</script>
