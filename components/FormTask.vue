<template>
  <v-card>
    <v-card-title>Nueva tarea</v-card-title>
    <v-card-text>
      <v-text-field label="Titulo" clearable v-model="title"></v-text-field>
      <v-text-field
        label="Descripción"
        clearable
        v-model="description"
      ></v-text-field>
      <v-btn
        style="backgroundColor: cornflowerblue;"
        block
        :disabled="isDisabled"
        @click="save"
        :loading="isLoading"
        >Enviar</v-btn
      >
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
      isDisabled: true,
      isLoading: false,
    };
  },
  watch: {
    title() {
      this.validate();
    },
    description() {
      this.validate();
    }
  },
  methods: {
    validate() {
      if (this.title.length > 0 && this.description.length > 0) {
        this.isDisabled = false;
      } else {
        this.isDisabled = true;
      }
    },
    async save() {
      this.isLoading = true;

      const hostname = "http://localhost:4800/tasks";
      const data = {
        title: this.title,
        description: this.description
      };

      const response = await fetch(hostname + "/create", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(data)
      });
      //const task = await response.json();
      //console.log({ task });
    
      this.$emit('taskCreated')
      this.isLoading = false;
    },

    
  }
};
</script>
