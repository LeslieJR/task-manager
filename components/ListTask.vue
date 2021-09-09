<template>
  <v-card>
    <v-card-title>{{ title }}</v-card-title>
    <v-card-text>{{ description }}</v-card-text>
    <v-card-actions>
      <v-btn style="backgroundColor: #65C97A; color:white" rounded @click="redirect">
        Edit
      </v-btn>
      <v-btn style="backgroundColor: #D75946; color:white" rounded @click="remove">
        Delete
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    }
  },
  methods:{
      async remove(){
          const hostname = "http://localhost:4800/tasks";
          await fetch(hostname+'/delete/'+this.id, 
          {method:'delete'})
          this.$emit('taskDeleted')
      },
      redirect(){
          this.$router.push(`/tasks/${this.id}`)
      }
  }
};
</script>
